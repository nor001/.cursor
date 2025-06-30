# SESSION PATTERNS - EFFICIENCY FOCUSED

## 🎯 **Special Cases I Don't Master**

### **SAP CSV Format (Headers on Line 3)**
```typescript
// I don't know this SAP format automatically
function processSAPCSV(csvData: string[]) {
  // Skip lines 1-2 (SAP metadata)
  // Headers on line 3
  // Data starts from line 4
  const headers = csvData[2].split(',');
  const data = csvData.slice(3).map(line => {
    const values = line.split(',');
    return headers.reduce((obj, header, index) => {
      obj[header.trim()] = values[index]?.trim();
      return obj;
    }, {} as any);
  });
  return data;
}
```

### **Corporate Environment Constraints**
```typescript
// I don't know corporate constraints automatically
function handleCorporateRequest(url: string) {
  // Corporate SSL requirements
  const httpsUrl = url.replace('http://', 'https://');
  
  // Proxy configuration needed
  const proxyConfig = {
    host: process.env.CORPORATE_PROXY_HOST,
    port: process.env.CORPORATE_PROXY_PORT,
    auth: process.env.CORPORATE_PROXY_AUTH
  };
  
  return fetch(httpsUrl, { 
    agent: new HttpsProxyAgent(proxyConfig) 
  });
}
```

## 🔧 **Build and Linting Patterns (I Don't Master)**

### **ESLint Error Resolution**
```typescript
// I don't know these specific fixes automatically
// 1. Unused variables → prefix with underscore
const { csvData, planType, assignedData: _assignedData } = get();

// 2. Console statements → replace with logError
// ❌ console.error('Error:', error);
// ✅ logError({ type: 'processing', message: 'Error occurred', details: error }, 'context');

// 3. Any types → create specific interfaces
interface SAPProjectData {
  fecha_inicio: string;
  fecha_fin: string;
  responsable: string;
  duracion: number;
}
```

### **Windows Dependency Recovery**
```powershell
# I don't know this Windows-specific recovery automatically
npm cache clean --force
Remove-Item -Recurse -Force node_modules -ErrorAction SilentlyContinue
npm install
npx next --version
```

## 🔍 **Debug Patterns (I Don't Master)**

### **Strategic Debug Logging**
```typescript
// I don't know this debug pattern automatically
function addDebugLogs(component: string, data: any) {
  console.log(`[DEBUG] ${component}:`, {
    dataLength: data?.length,
    filters: getCurrentFilters(),
    timestamp: new Date().toISOString()
  });
}
```

## 🛡️ **Business Logic Preservation (I Don't Master)**

### **Special Cases Detection**
```typescript
// I don't know to preserve special logic automatically
function identifySpecialCase(data, context) {
  if (hasFormatVariation(data)) return 'format_variation';
  if (hasCorporateConstraint(context)) return 'corporate_constraint';
  if (hasBusinessRule(data)) return 'business_rule';
  return 'default';
}

// ALWAYS preserve special cases
function handleSpecialCase(data, context) {
  const caseType = identifySpecialCase(data, context);
  
  switch (caseType) {
    case 'format_variation':
      return handleFormatVariation(data);
    case 'corporate_constraint':
      return handleCorporateConstraint(data);
    case 'business_rule':
      return handleBusinessRule(data);
    default:
      return handleDefaultCase(data);
  }
}
```

## 📚 **AI Rules - Special Cases Only**

### **AI Documentation Templates**
```typescript
// I don't know these special case tags automatically
/**
 * @ai-special-case csv_headers_line_3
 * @ai-context SAP CSV export format with headers on line 3
 * @ai-preserve ALWAYS preserve this special parsing logic
 */
```

### **AI Error Handling**
```typescript
// I don't know SAP-specific error handling automatically
interface AIErrorLog {
  timestamp: string;
  errorType: 'SAP_BUSINESS' | 'CORPORATE_CONSTRAINT' | 'LEGACY_FORMAT';
  errorCode: string;
  message: string;
  context: Record<string, any>;
}

async function handleSAPDataProcessing(data: any[]): Promise<ProcessingResult> {
  try {
    return await processSAPDataWithFullValidation(data);
  } catch (error) {
    logAIError(error, { action: 'SAP_DATA_PROCESSING' });
    
    // Graceful degradation for SAP data
    try {
      return await processSAPDataWithBasicValidation(data);
    } catch (fallbackError) {
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

### **AI Naming Patterns**
```typescript
// I don't know SAP naming patterns automatically
// ✅ AI-Friendly: Clear SAP domain context
const renderSAPTimelineView = () => { ... }
const handleSAPFilterChange = (filters: FilterState) => { ... }
POST /api/sap-projects/upload-csv
interface SAPProjectData { ... }
```

### **AI Integration**
```typescript
// I don't know this decision framework automatically
function applyRulesByContext(context: DevelopmentContext) {
  if (context.isEmergency) {
    return applyFallbackRules(); // UNIVERSAL-RULE fallback
  }
  
  if (context.hasSpecialCases) {
    return applySpecialCaseRules(); // Special case handling
  }
  
  return applyBasicRules(); // Basic UNIVERSAL-RULE
}
```

### **Security in Error Handling**
```typescript
// I don't know corporate security patterns automatically
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

---

## 📋 **Essential Checklists (Special Cases Only)**

### **Pre-Implementation**
- [ ] **SAP Special Cases**: Document CSV headers on line 3
- [ ] **Corporate Constraints**: Check SSL/Proxy requirements
- [ ] **Legacy Compatibility**: Verify legacy system requirements
- [ ] **Business Logic**: Preserve critical business rules

### **Post-Implementation**
- [ ] **Special Case Preservation**: Confirm SAP logic is intact
- [ ] **Corporate Compliance**: Validate corporate constraints
- [ ] **Legacy Compatibility**: Test legacy system compatibility
- [ ] **Business Logic**: Verify business rules are preserved

---

## 📊 **Core Metrics (Special Cases Focus)**

### **Special Case Handling**
- **SAP Format Recognition**: Correctly identify CSV line 3 format (Target: 100%)
- **Corporate Constraint Compliance**: Handle SSL/Proxy requirements (Target: 100%)
- **Legacy Compatibility**: Maintain legacy system compatibility (Target: 100%)
- **Business Logic Preservation**: Preserve critical business rules (Target: 100%) 