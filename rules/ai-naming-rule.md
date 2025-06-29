# AI NAMING CONVENTIONS - COMPLEMENT TO NORM-RULE

## 🎯 **Purpose**
This rule complements `norm-rule.md` with explicit AI-friendly naming conventions and patterns.

## 📝 **AI Naming Philosophy**

### **Core Principle: Context-Rich Naming**
- **Include domain context** in function and variable names
- **Use descriptive prefixes** that AI can understand
- **Maintain consistency** across the entire codebase
- **Balance descriptiveness** with readability

### **Naming Hierarchy**
1. **Domain Prefix** - Business domain (SAP, User, Auth, etc.)
2. **Action Verb** - What the function does (handle, validate, process, etc.)
3. **Context** - Specific context or data type
4. **Suffix** - Additional context if needed

## 🔧 **AI Naming Standards**

### **1. Function Naming Patterns**

#### **Business Logic Functions**
```typescript
// ✅ AI-Friendly: Clear domain and action
const handleSAPCSVFileUpload = (file: File) => { ... }
const validateSAPProjectData = (data: any[]) => { ... }
const processSAPResourceAssignment = () => { ... }
const calculateSAPProjectMetrics = (projects: Project[]) => { ... }

// ❌ Generic: No domain context
const uploadFile = (file: File) => { ... }
const validateData = (data: any[]) => { ... }
const processData = () => { ... }
const calculateMetrics = (data: any[]) => { ... }
```

#### **Component Functions**
```typescript
// ✅ AI-Friendly: Clear component purpose
const renderSAPTimelineView = () => { ... }
const handleSAPFilterChange = (filters: FilterState) => { ... }
const updateSAPProjectStatus = (projectId: string, status: string) => { ... }

// ❌ Generic: Unclear purpose
const renderView = () => { ... }
const handleChange = (data: any) => { ... }
const updateStatus = (id: string, value: any) => { ... }
```

### **2. Variable Naming Patterns**

#### **Business Data Variables**
```typescript
// ✅ AI-Friendly: Clear data context
const sapProjectData = [...];
const abapResourceList = [...];
const csvUploadStatus = 'idle';
const timelinePaginationState = { currentPage: 0, totalPages: 10 };

// ❌ Generic: No context
const data = [...];
const list = [...];
const status = 'idle';
const pagination = { page: 0, total: 10 };
```

#### **State Variables**
```typescript
// ✅ AI-Friendly: Clear state purpose
const [isSAPDataLoading, setIsSAPDataLoading] = useState(false);
const [sapProjectFilters, setSapProjectFilters] = useState(initialFilters);
const [timelineViewMode, setTimelineViewMode] = useState<'gantt' | 'table'>('gantt');

// ❌ Generic: Unclear state purpose
const [loading, setLoading] = useState(false);
const [filters, setFilters] = useState(initialFilters);
const [viewMode, setViewMode] = useState('gantt');
```

### **3. API Endpoint Naming**

#### **RESTful with Domain Context**
```typescript
// ✅ AI-Friendly: Clear domain and action
POST /api/sap-projects/upload-csv
GET /api/sap-projects/metadata
PUT /api/sap-resources/assign
DELETE /api/sap-projects/:id

// ❌ Generic: No domain context
POST /api/upload
GET /api/metadata
PUT /api/assign
DELETE /api/:id
```

### **4. Type and Interface Naming**

#### **Domain-Specific Types**
```typescript
// ✅ AI-Friendly: Clear domain context
interface SAPProjectData {
  fecha_inicio: string;
  fecha_fin: string;
  responsable: string;
  duracion: number;
}

interface ABAPResource {
  id: string;
  name: string;
  skills: string[];
  availability: DateRange;
}

// ❌ Generic: No domain context
interface ProjectData {
  startDate: string;
  endDate: string;
  assignee: string;
  duration: number;
}

interface Resource {
  id: string;
  name: string;
  capabilities: string[];
  schedule: DateRange;
}
```

## 🎯 **Naming Conventions by Domain**

### **SAP Domain**
```typescript
// Functions
handleSAPCSVUpload()
validateSAPProjectData()
processSAPResourceAssignment()
calculateSAPProjectMetrics()

// Variables
sapProjectData
sapResourceList
sapTimelineView
sapFilterState

// Types
SAPProjectData
SAPResource
SAPTimelineConfig
```

### **Authentication Domain**
```typescript
// Functions
handleUserAuthentication()
validateUserCredentials()
processUserLogin()
refreshUserToken()

// Variables
userAuthState
userCredentials
userSessionData
userPermissions

// Types
UserAuthData
UserCredentials
UserSession
```

### **UI/UX Domain**
```typescript
// Functions
handleModalOpen()
validateFormInput()
processUserInteraction()
updateUIState()

// Variables
modalState
formValidationErrors
userInteractionLog
uiThemeState

// Types
ModalState
FormValidation
UserInteraction
UITheme
```

## 🛠️ **Implementation Guidelines**

### **When to Use Domain Prefixes**
- ✅ **Business logic functions** that operate on domain data
- ✅ **API endpoints** that handle domain-specific operations
- ✅ **State variables** that represent domain state
- ✅ **Type definitions** for domain entities

### **When NOT to Use Domain Prefixes**
- ❌ **Utility functions** that are domain-agnostic
- ❌ **Generic helper functions** (formatDate, validateEmail, etc.)
- ❌ **Standard library functions** or third-party integrations
- ❌ **Configuration constants** that are already contextual

### **Prefix Priority**
1. **Primary Domain** - Main business domain (SAP, User, etc.)
2. **Sub-domain** - Specific area within domain (Project, Resource, etc.)
3. **Action Type** - Type of operation (Upload, Validate, Process, etc.)
4. **Data Type** - Type of data being handled (CSV, JSON, etc.)

## 🔄 **Integration with NORM-RULE**

### **Complementary Relationship**
- **NORM-RULE**: Provides operational framework and decision-making
- **AI-NAMING-RULE**: Provides naming standards for AI understanding
- **Together**: Create consistent, AI-friendly codebase

### **Shared Principles**
- **Security-first** approach in naming sensitive operations
- **Special case preservation** in naming edge case handlers
- **Direct action protocol** in naming action functions
- **Minimalist** but descriptive naming

### **Enhanced Workflow**
1. **NORM-RULE** determines operational approach
2. **AI-NAMING-RULE** ensures consistent, contextual naming
3. **Combined** result: AI-friendly code with clear operational context

## 📊 **Success Metrics**

### **AI Understanding Metrics**
- **Context Recognition**: AI correctly identifies function purpose
- **Domain Awareness**: AI understands business domain context
- **Action Clarity**: AI understands what functions do
- **Data Understanding**: AI understands data structure and purpose

### **Human Developer Metrics**
- **Readability**: Code is easy to read and understand
- **Maintainability**: Easy to modify and extend
- **Consistency**: Naming patterns are consistent across codebase
- **Onboarding**: New developers understand naming quickly

## 🚀 **Best Practices**

### **1. Progressive Naming**
```typescript
// Start with basic context
const handleUpload = (file: File) => { ... }

// Add domain context as needed
const handleCSVUpload = (file: File) => { ... }

// Add full context for complex operations
const handleSAPCSVFileUpload = (file: File) => { ... }
```

### **2. Consistent Patterns**
```typescript
// Use consistent patterns across the project
const handle[Domain][Action] = () => { ... }
const validate[Domain][DataType] = () => { ... }
const process[Domain][Operation] = () => { ... }
const calculate[Domain][Metric] = () => { ... }
```

### **3. Balance Descriptiveness**
```typescript
// ✅ Good: Descriptive but not verbose
const handleSAPProjectUpload = (file: File) => { ... }

// ❌ Too verbose: Unnecessarily long
const handleSAPProjectCSVFileUploadWithValidation = (file: File) => { ... }

// ❌ Too generic: No context
const handleUpload = (file: File) => { ... }
```

## 🎯 **Conclusion**

This AI naming rule **complements NORM-RULE** by providing explicit standards for AI-friendly naming conventions. Together, they create a comprehensive framework for AI-assisted development that maintains both AI understanding and human readability.

**Key Benefits:**
- ✅ **Explicit naming standards** for AI understanding
- ✅ **Consistent patterns** across the project
- ✅ **Domain-aware naming** for business context
- ✅ **Balanced approach** for AI and human needs
- ✅ **Integration** with existing NORM-RULE framework 