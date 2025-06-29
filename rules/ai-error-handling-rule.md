# AI ERROR HANDLING PATTERNS - COMPLEMENT TO NORM-RULE

## 🎯 **Purpose**
This rule complements `norm-rule.md` with explicit AI-friendly error handling patterns and standards.

## 📝 **AI Error Handling Philosophy**

### **Core Principle: Context-Rich Error Handling**
- **Provide context** that helps AI understand and resolve errors
- **Use structured error patterns** that AI can parse and understand
- **Maintain security** while providing useful debugging information
- **Enable AI-assisted debugging** through clear error categorization

### **Error Handling Hierarchy**
1. **Error Detection** - Identify and categorize errors
2. **Context Preservation** - Maintain relevant context for debugging
3. **AI-Friendly Logging** - Log in formats AI can understand
4. **Graceful Degradation** - Handle errors without breaking functionality
5. **Recovery Mechanisms** - Provide paths for error recovery

## 🔧 **AI Error Handling Standards**

### **1. Error Categorization System**

#### **Business Logic Errors**
```typescript
// ✅ AI-Friendly: Clear error categorization
class SAPBusinessError extends Error {
  constructor(
    message: string,
    public readonly errorCode: 'INVALID_PROJECT_DATA' | 'RESOURCE_CONFLICT' | 'TIMELINE_OVERLAP',
    public readonly context: {
      projectId?: string;
      resourceId?: string;
      dateRange?: { start: string; end: string };
    }
  ) {
    super(`SAP Business Error [${errorCode}]: ${message}`);
    this.name = 'SAPBusinessError';
  }
}

// Usage
throw new SAPBusinessError(
  'Project timeline overlaps with existing project',
  'TIMELINE_OVERLAP',
  { projectId: 'PROJ-001', dateRange: { start: '2024-01-01', end: '2024-03-01' } }
);
```

#### **Validation Errors**
```typescript
// ✅ AI-Friendly: Structured validation errors
class SAPValidationError extends Error {
  constructor(
    message: string,
    public readonly field: string,
    public readonly value: any,
    public readonly expectedFormat: string
  ) {
    super(`SAP Validation Error [${field}]: ${message}. Expected: ${expectedFormat}, Got: ${JSON.stringify(value)}`);
    this.name = 'SAPValidationError';
  }
}

// Usage
throw new SAPValidationError(
  'Invalid date format',
  'fecha_inicio',
  'invalid-date',
  'YYYY-MM-DD'
);
```

#### **System Errors**
```typescript
// ✅ AI-Friendly: System error with context
class SAPSystemError extends Error {
  constructor(
    message: string,
    public readonly operation: string,
    public readonly systemContext: {
      endpoint?: string;
      statusCode?: number;
      responseTime?: number;
    }
  ) {
    super(`SAP System Error [${operation}]: ${message}`);
    this.name = 'SAPSystemError';
  }
}

// Usage
throw new SAPSystemError(
  'Failed to connect to SAP system',
  'CSV_UPLOAD',
  { endpoint: '/api/sap-upload', statusCode: 500, responseTime: 5000 }
);
```

### **2. AI-Friendly Error Logging**

#### **Structured Error Logging**
```typescript
// ✅ AI-Friendly: Structured logging for AI analysis
interface AIErrorLog {
  timestamp: string;
  errorType: 'BUSINESS' | 'VALIDATION' | 'SYSTEM' | 'SECURITY';
  errorCode: string;
  message: string;
  context: Record<string, any>;
  stack?: string;
  userContext?: {
    userId?: string;
    sessionId?: string;
    action?: string;
  };
  systemContext?: {
    endpoint?: string;
    method?: string;
    userAgent?: string;
    ip?: string;
  };
}

function logAIError(error: Error, context: Partial<AIErrorLog>): void {
  const errorLog: AIErrorLog = {
    timestamp: new Date().toISOString(),
    errorType: determineErrorType(error),
    errorCode: extractErrorCode(error),
    message: error.message,
    context: extractErrorContext(error),
    stack: error.stack,
    ...context
  };
  
  console.error('AI_ERROR_LOG:', JSON.stringify(errorLog, null, 2));
}
```

#### **Error Context Extraction**
```typescript
// ✅ AI-Friendly: Extract context for AI analysis
function extractErrorContext(error: Error): Record<string, any> {
  if (error instanceof SAPBusinessError) {
    return {
      errorCode: error.errorCode,
      businessContext: error.context
    };
  }
  
  if (error instanceof SAPValidationError) {
    return {
      field: error.field,
      value: error.value,
      expectedFormat: error.expectedFormat
    };
  }
  
  if (error instanceof SAPSystemError) {
    return {
      operation: error.operation,
      systemContext: error.systemContext
    };
  }
  
  return { genericError: true };
}
```

### **3. Error Recovery Patterns**

#### **Graceful Degradation**
```typescript
// ✅ AI-Friendly: Graceful degradation with clear fallbacks
async function handleSAPDataProcessing(data: any[]): Promise<ProcessingResult> {
  try {
    // Primary processing path
    return await processSAPDataWithFullValidation(data);
  } catch (error) {
    logAIError(error, { action: 'SAP_DATA_PROCESSING' });
    
    // Graceful degradation: Try with basic validation
    try {
      return await processSAPDataWithBasicValidation(data);
    } catch (fallbackError) {
      logAIError(fallbackError, { action: 'SAP_DATA_FALLBACK' });
      
      // Final fallback: Return partial results
      return {
        success: false,
        data: data.filter(item => isValidBasicItem(item)),
        errors: [error.message, fallbackError.message],
        degraded: true
      };
    }
  }
}
```

#### **Retry Mechanisms**
```typescript
// ✅ AI-Friendly: Retry with exponential backoff
async function retryWithAIContext<T>(
  operation: () => Promise<T>,
  context: {
    operationName: string;
    maxRetries?: number;
    baseDelay?: number;
  }
): Promise<T> {
  const { operationName, maxRetries = 3, baseDelay = 1000 } = context;
  
  for (let attempt = 1; attempt <= maxRetries; attempt++) {
    try {
      return await operation();
    } catch (error) {
      logAIError(error, {
        action: operationName,
        context: { attempt, maxRetries, baseDelay }
      });
      
      if (attempt === maxRetries) {
        throw error;
      }
      
      // Exponential backoff
      const delay = baseDelay * Math.pow(2, attempt - 1);
      await new Promise(resolve => setTimeout(resolve, delay));
    }
  }
  
  throw new Error(`Operation ${operationName} failed after ${maxRetries} attempts`);
}
```

### **4. Error Response Patterns**

#### **API Error Responses**
```typescript
// ✅ AI-Friendly: Structured API error responses
interface AIErrorResponse {
  success: false;
  error: {
    type: 'BUSINESS' | 'VALIDATION' | 'SYSTEM' | 'SECURITY';
    code: string;
    message: string;
    context?: Record<string, any>;
    suggestions?: string[];
  };
  timestamp: string;
  requestId: string;
}

function createAIErrorResponse(
  error: Error,
  requestId: string
): AIErrorResponse {
  return {
    success: false,
    error: {
      type: determineErrorType(error),
      code: extractErrorCode(error),
      message: error.message,
      context: extractErrorContext(error),
      suggestions: generateErrorSuggestions(error)
    },
    timestamp: new Date().toISOString(),
    requestId
  };
}
```

#### **Error Suggestions for AI**
```typescript
// ✅ AI-Friendly: Generate suggestions for AI debugging
function generateErrorSuggestions(error: Error): string[] {
  const suggestions: string[] = [];
  
  if (error instanceof SAPValidationError) {
    suggestions.push(`Check if ${error.field} follows format: ${error.expectedFormat}`);
    suggestions.push(`Validate input data before processing`);
    suggestions.push(`Review data source for format inconsistencies`);
  }
  
  if (error instanceof SAPBusinessError) {
    suggestions.push(`Review business rules for ${error.errorCode}`);
    suggestions.push(`Check for conflicting data in context: ${JSON.stringify(error.context)}`);
    suggestions.push(`Validate business logic constraints`);
  }
  
  if (error instanceof SAPSystemError) {
    suggestions.push(`Check system connectivity for ${error.operation}`);
    suggestions.push(`Review system logs for detailed error information`);
    suggestions.push(`Verify system configuration and permissions`);
  }
  
  return suggestions;
}
```

## 🛠️ **Implementation Guidelines**

### **When to Use AI Error Handling**
- ✅ **Business logic errors** that need context for debugging
- ✅ **Validation errors** that need clear feedback
- ✅ **System errors** that need troubleshooting context
- ✅ **Security errors** that need careful logging
- ✅ **Integration errors** with external systems

### **When NOT to Use AI Error Handling**
- ❌ **Simple validation errors** with obvious solutions
- ❌ **Standard library errors** that are well understood
- ❌ **Third-party errors** that don't need custom handling
- ❌ **Performance-critical paths** where overhead is unacceptable

### **Error Handling Priority**
1. **Security Errors** - Handle with extra care and logging
2. **Business Logic Errors** - Provide context for debugging
3. **Validation Errors** - Give clear feedback for correction
4. **System Errors** - Enable troubleshooting and recovery
5. **Generic Errors** - Basic handling with minimal overhead

## 🔄 **Integration with NORM-RULE**

### **Complementary Relationship**
- **NORM-RULE**: Provides operational framework and decision-making
- **AI-ERROR-RULE**: Provides error handling standards for AI understanding
- **Together**: Create robust, AI-friendly error handling system

### **Shared Principles**
- **Security-first** approach in error handling
- **Special case preservation** in error contexts
- **Direct action protocol** in error recovery
- **Minimalist** but comprehensive error handling

### **Enhanced Workflow**
1. **NORM-RULE** determines operational approach
2. **AI-ERROR-RULE** ensures proper error handling and logging
3. **Combined** result: Robust system with AI-friendly debugging

## 📊 **Success Metrics**

### **AI Understanding Metrics**
- **Error Recognition**: AI correctly identifies error types
- **Context Understanding**: AI understands error context
- **Recovery Suggestions**: AI provides useful debugging suggestions
- **Pattern Recognition**: AI recognizes error patterns across system

### **Human Developer Metrics**
- **Debugging Speed**: Errors are easy to identify and resolve
- **Error Prevention**: Clear error patterns prevent future issues
- **System Reliability**: Graceful degradation maintains functionality
- **Monitoring**: Comprehensive error logging enables monitoring

## 🚀 **Best Practices**

### **1. Progressive Error Handling**
```typescript
// Start with basic error handling
try {
  return await operation();
} catch (error) {
  console.error('Operation failed:', error);
  throw error;
}

// Add AI-friendly context as needed
try {
  return await operation();
} catch (error) {
  logAIError(error, { action: 'OPERATION_NAME' });
  throw error;
}

// Add recovery mechanisms for critical operations
try {
  return await operation();
} catch (error) {
  logAIError(error, { action: 'OPERATION_NAME' });
  return await fallbackOperation();
}
```

### **2. Consistent Error Patterns**
```typescript
// Use consistent error patterns across the project
class DomainBusinessError extends Error {
  constructor(message: string, errorCode: string, context: any) {
    super(`Domain Business Error [${errorCode}]: ${message}`);
    this.name = 'DomainBusinessError';
    // ... additional properties
  }
}

class DomainValidationError extends Error {
  constructor(message: string, field: string, value: any, expectedFormat: string) {
    super(`Domain Validation Error [${field}]: ${message}`);
    this.name = 'DomainValidationError';
    // ... additional properties
  }
}
```

### **3. Security in Error Handling**
```typescript
// Always sanitize error information for security
function sanitizeErrorForLogging(error: Error): Error {
  const sanitizedError = new Error(error.message);
  sanitizedError.name = error.name;
  
  // Remove sensitive information from stack traces
  if (error.stack) {
    sanitizedError.stack = error.stack
      .split('\n')
      .filter(line => !line.includes('password') && !line.includes('token'))
      .join('\n');
  }
  
  return sanitizedError;
}
```

## 🎯 **Conclusion**

This AI error handling rule **complements NORM-RULE** by providing explicit standards for AI-friendly error handling patterns. Together, they create a comprehensive framework for AI-assisted development that maintains both AI understanding and human debugging capabilities.

**Key Benefits:**
- ✅ **Explicit error handling standards** for AI understanding
- ✅ **Structured error patterns** across the project
- ✅ **Context-rich error logging** for AI analysis
- ✅ **Graceful degradation** and recovery mechanisms
- ✅ **Integration** with existing NORM-RULE framework 