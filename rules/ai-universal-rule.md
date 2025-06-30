# AI Universal Rule - Optimized

# 🚨 MANDATORY RULE NAME DISPLAY
# ALWAYS start every response with the active rule name:
# [norm]

## 🎯 **Purpose**
3 essential rules + 2 cognitive modes - minimal overhead, maximum efficiency.

## 🎯 Core Rules (3 Essential)

### 1. Execute by Default
- **Default behavior**: Direct implementation without questions
- **Ask only for**: Business logic changes, architecture decisions, destructive operations
- **Mode distribution**: 25% execute, 75% think (complex project reality)

### 2. Domain-Specific Naming
- **Web**: React/Next.js patterns, component-based structure
- **Mobile**: React Native, Flutter, native patterns
- **Script**: Universal solutions, minimal validation overhead
- **Enterprise**: Domain-specific patterns, corporate constraints
- **Auto-detect**: Based on file extensions and request keywords

### 3. Special Cases Preservation
- **Never remove**: Special parsing logic, business rules, corporate constraints
- **Always preserve**: Legacy compatibility, format variations, edge cases
- **Document**: Special cases in code comments

## 🧠 Cognitive Modes (2 Modes)

### EXECUTE (25% of time)
- **Triggers**: Direct requests, error fixes, code improvements
- **Behavior**: Immediate implementation, minimal analysis
- **AI Style**: AI efficiency (faster processing, fewer tokens)

### THINK (75% of time)  
- **Triggers**: 'architecture', 'design', 'strategy', 'complex', 'special', 'corporate', 'legacy', 'integration', 'business logic', 'validation', 'project'
- **Behavior**: Analysis first, then implementation
- **AI Style**: AI friendly (clarity, maintainability)

## 🔄 Auto-Detection

### Mode Detection
```typescript
function detectMode(request: string): 'EXECUTE' | 'THINK' {
  const thinkTriggers = [
    'architecture', 'design', 'strategy', 
    'complex', 'special', 'corporate', 'legacy',
    'integration', 'business logic', 'validation',
    'project', 'planning', 'resource', 'system'
  ];
  
  return thinkTriggers.some(trigger => request.includes(trigger))
    ? 'THINK' 
    : 'EXECUTE';
}
```

### Domain Detection
```typescript
function detectDomain(request: string): 'WEB' | 'MOBILE' | 'SCRIPT' | 'ENTERPRISE' {
  const webTriggers = ['react', 'next', 'vue', 'angular', 'component', 'frontend'];
  const mobileTriggers = ['react-native', 'flutter', 'mobile', 'app', 'ios', 'android'];
  const scriptTriggers = ['script', 'batch', 'shell', 'python', 'automation'];
  const enterpriseTriggers = ['enterprise', 'corporate', 'legacy', 'integration', 'system'];
  
  if (mobileTriggers.some(trigger => request.includes(trigger))) {
    return 'MOBILE';
  }
  
  if (scriptTriggers.some(trigger => request.includes(trigger))) {
    return 'SCRIPT';
  }
  
  if (enterpriseTriggers.some(trigger => request.includes(trigger))) {
    return 'ENTERPRISE';
  }
  
  return 'WEB'; // Default
}
```

### Enterprise Complexity Detection
```typescript
function detectEnterpriseComplexity(request: string): 'SIMPLE' | 'COMPLEX' | 'CRITICAL' {
  const enterpriseTriggers = [
    'microservice', 'orchestration', 'saga', 'cqrs',
    'distributed', 'eventual_consistency', 'compensation',
    'circuit_breaker', 'bulkhead', 'timeout',
    'enterprise', 'corporate', 'legacy', 'integration'
  ];
  
  const criticalTriggers = [
    'production', 'live', 'critical', 'breaking_change',
    'data_migration', 'system_integration', 'compliance'
  ];
  
  if (criticalTriggers.some(trigger => request.includes(trigger))) {
    return 'CRITICAL';
  }
  
  if (enterpriseTriggers.some(trigger => request.includes(trigger))) {
    return 'COMPLEX';
  }
  
  return 'SIMPLE';
}
```

### AI Approach Selection
```typescript
const MODE_TO_APPROACH = {
  'EXECUTE': 'AI_EFFICIENCY',  // 25% - Fast execution for simple cases
  'THINK': 'AI_FRIENDLY'       // 75% - Clear analysis for complex cases
};

function selectApproach(request: string): 'AI_EFFICIENCY' | 'AI_FRIENDLY' {
  const mode = detectMode(request);
  const complexity = detectEnterpriseComplexity(request);
  
  // Auto-upgrade to AI_FRIENDLY for enterprise complexity
  if (complexity === 'COMPLEX' || complexity === 'CRITICAL') {
    return 'AI_FRIENDLY';
  }
  
  return MODE_TO_APPROACH[mode];
}
```

## 🏗️ Architecture-First for Enterprise

### Complexity Tiers
```typescript
const COMPLEXITY_TIERS = {
  SIMPLE: {
    approach: 'memory_sufficient',
    aiStyle: 'AI_EFFICIENCY',
    documentation: 'minimal'
  },
  COMPLEX: {
    approach: 'ai_analysis_required',
    aiStyle: 'AI_FRIENDLY',
    documentation: 'architecture_decision_record'
  },
  CRITICAL: {
    approach: 'full_context_ai',
    aiStyle: 'AI_FRIENDLY',
    documentation: 'comprehensive_adr'
  }
};
```

### Enterprise Context Injection
```typescript
interface EnterpriseContext {
  systemImpact: 'isolated' | 'cross_system' | 'critical_path';
  dataFlow: 'simple' | 'distributed' | 'eventual_consistency';
  businessCriticality: 'low' | 'medium' | 'high';
}

function injectEnterpriseContext(request: string): EnterpriseContext {
  const context: EnterpriseContext = {
    systemImpact: 'isolated',
    dataFlow: 'simple',
    businessCriticality: 'low'
  };
  
  // Auto-detect context based on request
  if (request.includes('distributed') || request.includes('microservice')) {
    context.dataFlow = 'distributed';
  }
  
  if (request.includes('critical') || request.includes('production')) {
    context.businessCriticality = 'high';
  }
  
  if (request.includes('integration') || request.includes('cross_system')) {
    context.systemImpact = 'cross_system';
  }
  
  return context;
}
```

### Enterprise Flow
```typescript
function enterpriseFlow(request: string) {
  const complexity = detectEnterpriseComplexity(request);
  
  if (complexity === 'COMPLEX' || complexity === 'CRITICAL') {
    return [
      '1. architectural_impact_analysis',
      '2. dependency_mapping',
      '3. integration_point_identification', 
      '4. implementation_with_monitoring'
    ];
  }
  
  return ['direct_implementation'];
}
```

## 👤 User Profile (3 Essential Fields)

### Core Traits
- **Style**: Analytical, optimization-focused, senior developer
- **Communication**: Direct, structured, efficiency-oriented  
- **Adaptation**: Auto-detect and adjust to user's interaction patterns

### Performance Caching
```typescript
const sessionCache = {
  userProfile: 'cache_per_session',        // No re-detection
  domainPattern: 'cache_per_project',      // Maintain project context
  commonTriggers: 'precompute_frequent'    // Pre-compute common patterns
};
```

## 🎯 Success Metrics

### Performance
- **Token reduction**: 30% fewer tokens (adjusted for complex reality)
- **Processing time**: 40% faster (balanced for analysis)
- **Decision points**: 50% fewer triggers

### Quality
- **Functionality preserved**: All core features maintained
- **Maintainability**: Clear, readable code
- **Adoption**: Simple enough for daily use
- **Special cases**: Excellent preservation with 75% THINK mode
- **Complex analysis**: Adequate time for project complexity
- **Enterprise patterns**: Auto-detection and appropriate handling

## 🎯 **3 ESSENTIAL RULES**

### **1. ⚡ EXECUTE BY DEFAULT**
```typescript
// ALWAYS proceed directly with requested tasks
// ONLY ask for: business logic changes, architecture decisions, destructive operations

function handleRequest(request: string) {
  const mode = detectMode(request);
  
  if (mode === 'THINK') {
    return analyzeThenExecute(request);
  }
  
  return executeDirectly(request); // Default - no questions
}
```

### **2. 🏷️ DOMAIN NAMING**
```typescript
// Domain-specific naming - I don't master this automatically

// Web Domain  
const useProjectData = () => { ... }
const handleFileUpload = (file: File) => { ... }
const ProjectService = class { ... }

// Script Domain
const script_process_csv = (file: string) => { ... }
const var_project_data = { ... }

// I don't know to use domain prefixes automatically
// ❌ uploadFile, validateData, processData (generic)
// ✅ useProjectData, handleFileUpload, script_process_csv (domain-specific)
```

### **3. 🛡️ PRESERVE SPECIAL CASES**
```typescript
// ALWAYS preserve special logic - I don't master this automatically

// Corporate Constraints
function handleCorporateRequest(url: string) {
  // Corporate SSL requirements
  // Proxy configuration needed
  // Legacy system compatibility
}

// NEVER remove special case handling without explicit confirmation
```

## 🏷️ **DOMAIN DETECTION (Minimal)**

### **Automatic Domain Detection**
```typescript
function detectDomain(request: string): 'WEB' | 'MOBILE' | 'SCRIPT' | 'ENTERPRISE' {
  const webTriggers = ['react', 'next', 'vue', 'angular', 'component', 'frontend'];
  const mobileTriggers = ['react-native', 'flutter', 'mobile', 'app', 'ios', 'android'];
  const scriptTriggers = ['script', 'batch', 'shell', 'python', 'automation'];
  const enterpriseTriggers = ['enterprise', 'corporate', 'legacy', 'integration', 'system'];
  
  if (mobileTriggers.some(trigger => request.includes(trigger))) {
    return 'MOBILE';
  }
  
  if (scriptTriggers.some(trigger => request.includes(trigger))) {
    return 'SCRIPT';
  }
  
  if (enterpriseTriggers.some(trigger => request.includes(trigger))) {
    return 'ENTERPRISE';
  }
  
  return 'WEB'; // Default
}
```

### **Domain Patterns (Minimal)**
```typescript
const DOMAIN_PATTERNS = {
  WEB: {
    naming: { components: 'use', handlers: 'handle' },
    patterns: { component_structure: "function_component_with_hooks" }
  },
  
  SCRIPT: {
    naming: { files: 'script_', functions: 'exec' },
    patterns: { create_file: true, prefer_cross_platform: true }
  }
};
```

## 📊 **EFFICIENCY METRICS (Minimal)**

### **Performance Tracking**
```typescript
interface EfficiencyMetrics {
  responseTime: number;
  tokenUsage: number;
  complexity: 'low' | 'medium' | 'high';
}

function provideMetrics(request: string): EfficiencyMetrics {
  return {
    responseTime: calculateResponseTime(),
    tokenUsage: calculateTokenUsage(),
    complexity: assessComplexity(request)
  };
}
```

## 📚 **Domain-Specific References**

### **For Web Development**
- See `.cursor/web-rule.md` for React, Next.js, and frontend patterns
- Performance auditing and API optimization
- Client-side caching and state management
- Browser-specific constraints

### **For Mobile Development**
- See `.cursor/mobile-rule.md` for React Native, Flutter patterns
- Platform-specific optimizations
- Cross-platform compatibility
- Performance considerations

### **For Script Development**
- Apply ULTRA-DIRECT PROTOCOL
- Prefer universal solutions over platform-specific
- Minimize validation overhead
- Focus on immediate execution

### **For Enterprise Development**
- See `.cursor/enterprise-rule.md` for enterprise patterns
- Integration strategies
- Data consistency patterns
- Corporate constraints

## 📚 **For Detailed Examples**
See `session-patterns.md` for special case implementation details. 

## 🔧 Implementation

### Automatic Application
- **No manual activation needed**
- **Auto-detect mode and domain**
- **Auto-upgrade to enterprise mode when needed**
- **Apply appropriate AI style**
- **Cache for performance**

### Manual Override Examples
```bash
# Real-world usage examples:
"complexity: critical"     # Force CRITICAL enterprise mode
"domain: enterprise"       # Force ENTERPRISE patterns
"mode: think"             # Force THINK mode
"mode: execute"           # Force EXECUTE mode
"domain: web"             # Force WEB patterns
"domain: mobile"          # Force MOBILE patterns
"domain: script"          # Force SCRIPT patterns
```

## 📚 Domain Patterns

### Web Development
- React/Next.js best practices
- Component-based architecture
- Performance optimization
- Modern UI/UX patterns

### Mobile Development
- React Native/Flutter patterns
- Native platform considerations
- Performance optimization
- Cross-platform compatibility

### Script Development  
- Universal compatibility
- Minimal dependencies
- Direct execution
- Error handling

### Enterprise Development
- Microservices patterns
- Event-driven architectures
- Data consistency patterns
- Integration patterns

## 📚 References

### For Detailed Examples
See `session-patterns.md` for special case implementation details.

### For Web Development
- See `.cursor/web-rule.md` for React, Next.js, and frontend patterns
- Performance auditing and API optimization
- Client-side caching and state management
- Browser-specific constraints

### For Mobile Development
- See `.cursor/mobile-rule.md` for React Native, Flutter patterns
- Platform-specific optimizations
- Cross-platform compatibility
- Performance considerations

### For Script Development
- Apply ULTRA-DIRECT PROTOCOL
- Prefer universal solutions over platform-specific
- Minimize validation overhead
- Focus on immediate execution

### For Enterprise Development
- See `.cursor/enterprise-rule.md` for enterprise patterns
- Integration strategies
- Data consistency patterns
- Corporate constraints