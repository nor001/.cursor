# AI DOCUMENTATION STANDARDS - COMPLEMENT TO NORM-RULE

## 🎯 **Purpose**
This rule complements `norm-rule.md` with explicit AI documentation standards and patterns.

## 📝 **AI Documentation Philosophy**

### **Core Principle: AI-First Documentation**
- **Document for AI understanding** first, human reading second
- **Use structured tags** that AI can parse and understand
- **Provide context** that helps AI make better decisions
- **Maintain human readability** while optimizing for AI

### **Documentation Hierarchy**
1. **AI Context Tags** - For AI understanding
2. **Functional Description** - For human developers
3. **Technical Details** - For implementation
4. **Business Context** - For domain understanding

## 🔧 **AI Documentation Standards**

### **1. Component Documentation Template**
```typescript
/**
 * @ai-context [What this component does in business terms]
 * @ai-purpose [Specific functionality and goals]
 * @ai-data-expects [Input data structure and format]
 * @ai-business-context [Business domain and rules]
 * @ai-special-cases [Edge cases and special handling]
 * @ai-cognitive-load [low|medium|high] - [explanation]
 * @ai-focus-state [clear|fuzzy|scattered] - [explanation]
 * @ai-session-type [standard|complex|crisis] - [explanation]
 * @ai-performance-notes [Performance considerations]
 * @ai-error-handling [Error handling approach]
 */
```

### **2. Function Documentation Template**
```typescript
/**
 * @ai-function [What this function does]
 * @ai-params [parameter descriptions]
 * @ai-returns [return value description]
 * @ai-business-rules [Business logic and constraints]
 * @ai-special-cases [Edge cases and exceptions]
 * @ai-performance-impact [Performance considerations]
 */
```

### **3. API Endpoint Documentation Template**
```typescript
/**
 * @ai-context [API endpoint purpose]
 * @ai-purpose [Specific functionality]
 * @ai-data-expects [Expected request format]
 * @ai-business-context [Business domain]
 * @ai-special-cases [Special handling required]
 * @ai-error-handling [Error response format]
 * @ai-security-notes [Security considerations]
 */
```

## 🎯 **AI Context Tags Reference**

### **Cognitive Load Tags**
```typescript
@ai-cognitive-load low    // Simple, straightforward logic
@ai-cognitive-load medium // Moderate complexity, multiple states
@ai-cognitive-load high   // Complex logic, many edge cases
```

### **Focus State Tags**
```typescript
@ai-focus-state clear     // Well-defined, predictable logic
@ai-focus-state fuzzy     // Ambiguous or unclear logic
@ai-focus-state scattered // Multiple concerns, complex flow
```

### **Session Type Tags**
```typescript
@ai-session-type standard // Routine operation
@ai-session-type complex  // Complex task requiring attention
@ai-session-type crisis   // Critical issue requiring immediate action
```

## 🛠️ **Implementation Guidelines**

### **When to Use AI Documentation**
- ✅ **Complex business logic** that's not obvious
- ✅ **Special cases** and edge case handling
- ✅ **Performance-critical** components
- ✅ **Security-sensitive** operations
- ✅ **Integration points** with external systems

### **When NOT to Use AI Documentation**
- ❌ **Simple utility functions** with obvious purpose
- ❌ **Standard patterns** that are well understood
- ❌ **Basic CRUD operations** without special logic
- ❌ **Self-explanatory** code with clear naming

### **Documentation Priority**
1. **Business Logic** - Document complex business rules
2. **Special Cases** - Document edge cases and exceptions
3. **Performance** - Document performance considerations
4. **Security** - Document security implications
5. **Integration** - Document external system interactions

## 🔄 **Integration with NORM-RULE**

### **Complementary Relationship**
- **NORM-RULE**: Provides operational framework and decision-making
- **AI-DOC-RULE**: Provides documentation standards for AI understanding
- **Together**: Create comprehensive AI-friendly development environment

### **Shared Principles**
- **Security-first** approach
- **Special case preservation**
- **Direct action protocol**
- **Minimalist documentation** philosophy

### **Enhanced Workflow**
1. **NORM-RULE** determines operational layer and approach
2. **AI-DOC-RULE** ensures proper documentation for AI understanding
3. **Combined** result: AI-friendly code with clear operational context

## 📊 **Success Metrics**

### **AI Understanding Metrics**
- **Context Recognition**: AI correctly identifies component purpose
- **Special Case Handling**: AI preserves critical business logic
- **Performance Awareness**: AI considers performance implications
- **Security Compliance**: AI maintains security standards

### **Human Developer Metrics**
- **Readability**: Code remains readable for human developers
- **Maintainability**: Easy to modify and extend
- **Onboarding**: New developers understand quickly
- **Debugging**: Issues are easy to identify and resolve

## 🚀 **Best Practices**

### **1. Balance AI and Human Needs**
```typescript
// ✅ Good: Balances AI context with human readability
/**
 * @ai-context SAP project timeline visualization
 * @ai-cognitive-load medium - Multiple states and pagination
 * 
 * Componente Timeline para visualización de proyectos SAP.
 * Maneja datasets grandes con paginación y filtrado por recursos ABAP.
 */

// ❌ Bad: Too much AI context, loses human readability
/**
 * @ai-context [very long technical description]
 * @ai-purpose [very long purpose description]
 * @ai-data-expects [very long data description]
 * // ... many more tags without human context
 */
```

### **2. Progressive Documentation**
```typescript
// Start with basic AI context
/**
 * @ai-context User authentication component
 */

// Add more context as complexity increases
/**
 * @ai-context User authentication with corporate SSO
 * @ai-special-cases Handles expired tokens and corporate policies
 * @ai-security-notes Validates against corporate directory
 */
```

### **3. Consistent Patterns**
```typescript
// Use consistent tag ordering across the project
/**
 * @ai-context [always first]
 * @ai-purpose [always second]
 * @ai-data-expects [always third]
 * @ai-business-context [always fourth]
 * @ai-special-cases [always fifth]
 * // ... other tags as needed
 */
```

## 🎯 **Conclusion**

This AI documentation rule **complements NORM-RULE** by providing explicit standards for AI-friendly documentation. Together, they create a comprehensive framework for AI-assisted development that maintains both AI understanding and human readability.

**Key Benefits:**
- ✅ **Explicit AI documentation standards**
- ✅ **Consistent patterns** across the project
- ✅ **Balanced approach** for AI and human needs
- ✅ **Progressive documentation** based on complexity
- ✅ **Integration** with existing NORM-RULE framework 