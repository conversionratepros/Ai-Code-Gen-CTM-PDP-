# CRO Template Structure - Technical Documentation

## Executive Summary

This repository implements a standardized, AI-optimized structure for managing Conversion Rate Optimization (CRO) experiments across multiple client websites. The architecture is designed to enable AI assistants to quickly understand template contexts, access proven patterns, and generate appropriate JavaScript/CSS code while avoiding known issues.

## System Architecture Overview

```
┌─────────────────────────────────────────────────────────────────┐
│                         Repository Root                          │
├─────────────────────────────────────────────────────────────────┤
│                                                                   │
│  ┌──────────────┐  ┌──────────────┐  ┌──────────────┐          │
│  │  /templates/ │  │   /shared/   │  │   /tools/    │          │
│  │              │  │              │  │              │          │
│  │  Client-     │  │  Cross-      │  │  Automation  │          │
│  │  specific    │◄─┤  template    │◄─┤  &           │          │
│  │  templates   │  │  utilities   │  │  Validation  │          │
│  └──────────────┘  └──────────────┘  └──────────────┘          │
│                            ▲                                     │
│                            │                                     │
│                    ┌──────────────┐                            │
│                    │ /.ai-config/ │                            │
│                    │              │                            │
│                    │ AI behavior  │                            │
│                    │ & prompting  │                            │
│                    └──────────────┘                            │
└─────────────────────────────────────────────────────────────────┘
```

## Core Design Principles

1. **Template Isolation**: Each client template is completely self-contained
2. **AI-First Documentation**: Every file is optimized for AI parsing and understanding
3. **Pattern Reusability**: Successful patterns are captured and indexed for reuse
4. **Progressive Enhancement**: Start with baseline, layer experiments on top
5. **Defensive Coding**: All patterns account for async loading and DOM volatility

## Directory Structure Detailed Breakdown

### 🎯 `/templates/[template-name]/`
**Purpose**: Container for all client-specific template information and experiments

#### `README.md`
- **Purpose**: Template overview and quick reference
- **Contents**: 
  - Technical stack (frameworks, libraries, analytics)
  - Key pages and their URLs
  - Dependencies and version requirements
  - Quick start instructions
- **Usage**: First file AI reads to understand the template context

#### `baseline.html`
- **Purpose**: Clean, annotated HTML structure of the template
- **Contents**: 
  - Semantic HTML with data attributes
  - Component boundaries marked with `data-component`
  - Interactive elements marked with `data-action`
  - Comments indicating dynamic/async loaded sections
- **Usage**: Reference for understanding DOM structure without runtime modifications

### 📚 `/templates/[template-name]/docs/`
**Purpose**: Comprehensive documentation for AI to understand the template

#### `architecture.md`
- **Purpose**: High-level technical architecture documentation
- **Contents**:
  - Component hierarchy diagram
  - Data flow patterns (events, state management)
  - Framework-specific patterns (React lifecycle, Vue reactivity)
  - Performance considerations
  - Browser compatibility requirements
- **Usage**: AI uses this to understand how components interact

#### `selectors.json`
- **Purpose**: Complete DOM element mapping
- **Structure**:
```json
{
  "componentName": {
    "selector": "CSS selector",
    "alternativeSelectors": ["fallback selectors"],
    "jsHook": "JavaScript variable or function",
    "asyncLoad": true/false,
    "loadTime": "milliseconds",
    "children": { nested elements }
  }
}
```
- **Usage**: AI references this for reliable element selection

#### `components.md`
- **Purpose**: Detailed documentation of reusable UI components
- **Contents**:
  - Component API (props, methods, events)
  - Styling hooks and CSS classes
  - State management approach
  - Integration examples
- **Usage**: Understanding existing components before modifying

#### `style-tokens.json`
- **Purpose**: Design system tokens and CSS variables
- **Structure**:
```json
{
  "colors": { "primary": "#hex", "secondary": "#hex" },
  "breakpoints": { "mobile": "768px", "desktop": "1024px" },
  "animations": { "fadeIn": "0.3s ease-in" },
  "zIndex": { "modal": 9999, "header": 1000 }
}
```
- **Usage**: Maintaining visual consistency in experiments

#### `gotchas.md`
- **Purpose**: Document known issues and edge cases
- **Format**:
```markdown
## Issue Name
**Symptoms**: What goes wrong
**Cause**: Why it happens
**Solution**: How to fix/avoid
**Affected Elements**: Selectors impacted
```
- **Usage**: AI checks this before implementing solutions

#### `fixes.json`
- **Purpose**: Structured collection of proven solutions
- **Structure**:
```json
{
  "fixes": [{
    "id": "unique-identifier",
    "issue": "Problem description",
    "symptoms": ["array of symptoms"],
    "selector": "affected element",
    "solution": "code or approach",
    "context": "when this applies",
    "priority": 1-5
  }]
}
```
- **Usage**: Pattern matching for automatic problem resolution

#### `conversions.md`
- **Purpose**: Track what drives conversions for this template
- **Contents**:
  - Primary and secondary KPIs
  - Successful experiment patterns
  - Failed approaches to avoid
  - User behavior insights
- **Usage**: Informing hypothesis generation

### 🧪 `/templates/[template-name]/experiments/[TICKET-ID]/`
**Purpose**: Complete documentation of individual experiments

#### `README.md`
- **Purpose**: Experiment overview
- **Contents**: Hypothesis, success metrics, stakeholders

#### `spec.yaml`
- **Purpose**: Detailed technical requirements
- **Structure**:
```yaml
experiment:
  id: "TICKET-ID"
  name: "Experiment Name"
  targeting:
    urls: ["regex patterns"]
    audience: "segment definition"
  variants:
    control: "baseline"
    treatment: "changes description"
  metrics:
    primary: "conversion"
    secondary: ["engagement", "revenue"]
```

#### `plan.md`
- **Purpose**: Implementation strategy
- **Contents**: Step-by-step approach, risk assessment, QA checklist

#### `variant.js`
- **Purpose**: JavaScript implementation
- **Standards**: 
  - IIFE pattern for scope isolation
  - Defensive DOM selection
  - Event listener cleanup
  - Error handling

#### `variant.css`
- **Purpose**: Style modifications
- **Standards**:
  - High specificity selectors
  - !important when necessary
  - Mobile-first responsive design

#### `corrections.md`
- **Purpose**: Post-launch fixes and iterations
- **Format**: Dated entries with issue→solution mapping

#### `results.md`
- **Purpose**: Experiment outcomes
- **Contents**: Statistical significance, learnings, recommendations

### 🔧 `/templates/[template-name]/components/`
**Purpose**: Reusable component library specific to this template

Each component folder contains:
- `component.js` - JavaScript implementation
- `component.css` - Styles
- `component.md` - Documentation
- `component.test.js` - Unit tests (optional)

### 🛠 `/templates/[template-name]/utilities/`
**Purpose**: Template-specific helper functions

#### `helpers.js`
- Common utility functions (debounce, throttle, formatters)

#### `constants.js`
- Template-specific constants (API endpoints, config values)

#### `validators.js`
- Form validation, data sanitization functions

### 🧠 `/templates/[template-name]/index/`
**Purpose**: AI-optimized knowledge indexing

#### `embeddings/`
- **Purpose**: Vector representations for semantic search
- **Files**:
  - `components.json` - Component embeddings
  - `patterns.json` - Pattern embeddings
- **Usage**: AI similarity search for relevant code

#### `memory/`
- **Purpose**: Accumulated knowledge from experiments
- **Files**:
  - `successful-patterns.md` - What worked
  - `failed-patterns.md` - What didn't work
  - `macros/` - Reusable code snippets

### 🌐 `/shared/`
**Purpose**: Cross-template shared resources

#### `utilities/`
- `analytics.js` - Universal tracking implementations
- `ab-testing.js` - Testing platform helpers
- `dom-utilities.js` - Common DOM operations (waitForElement, etc.)

#### `styles/`
- `reset.css` - CSS normalizations
- `utilities.css` - Utility classes (.hidden, .sr-only)

#### `documentation/`
- `coding-standards.md` - Team code style guide
- `ai-instructions.md` - How AI should interact with the repo
- `experiment-workflow.md` - Process documentation

### 🤖 `/.ai-config/`
**Purpose**: AI-specific configuration and instructions

#### `prompts/`
- `code-generation.md` - Instructions for generating code
- `review-checklist.md` - Pre-implementation checklist
- `context-gathering.md` - How to analyze the repository

#### `rules.json`
```json
{
  "rules": {
    "always_check_selectors": true,
    "use_defensive_coding": true,
    "check_gotchas_first": true,
    "prefer_memory_patterns": true,
    "max_specificity_increase": 2,
    "require_error_handling": true
  }
}
```

### 🔨 `/tools/`
**Purpose**: Development and maintenance utilities

#### `validators/`
- `validate-structure.js` - Ensures folder structure compliance
- `validate-experiment.js` - Checks experiment completeness

#### `generators/`
- `new-template.js` - Scaffolds new client template
- `new-experiment.js` - Creates experiment boilerplate

## Workflow Integration

### For Developers

1. **Starting a New Client**:
   ```bash
   node tools/generators/new-template.js --name "client-name"
   ```

2. **Creating an Experiment**:
   ```bash
   node tools/generators/new-experiment.js --template "client-name" --id "CRO-1234"
   ```

3. **Validation Before Commit**:
   ```bash
   node tools/validators/validate-structure.js
   ```

### For AI Assistants

1. **Context Gathering Flow**:
   ```
   Read template README.md
   → Parse docs/architecture.md
   → Load docs/selectors.json
   → Check docs/gotchas.md
   → Review relevant experiments/
   → Check memory/successful-patterns.md
   ```

2. **Code Generation Flow**:
   ```
   Identify required selectors
   → Check for existing components
   → Apply fixes from fixes.json
   → Use patterns from memory/
   → Generate defensive code
   → Include error handling
   ```

## Best Practices

### Documentation Standards
- Use Markdown for human-readable docs
- Use JSON for structured data
- Keep examples in documentation current
- Document failures as thoroughly as successes

### Code Standards
- All JavaScript in IIFE to avoid global scope pollution
- Use `data-*` attributes for JavaScript hooks, not classes
- CSS specificity should be as low as possible while still working
- Always include mobile-responsive considerations

### Experiment Standards
- One experiment per folder
- Use ticket IDs for folder names
- Document hypothesis before implementation
- Track results even if experiment fails

### AI Optimization
- Keep selectors.json updated with any DOM changes
- Add new patterns to memory/ after successful experiments
- Update gotchas.md when discovering new issues
- Maintain fixes.json as the source of truth for solutions

## Maintenance Guidelines

### Weekly Tasks
- Review and update gotchas.md with new findings
- Archive completed experiments older than 3 months
- Update successful patterns in memory/

### Monthly Tasks
- Validate all selectors still work
- Review and consolidate fixes.json
- Update component documentation
- Generate embeddings for new patterns

### Per Experiment
- Create experiment folder before starting
- Update components/ if creating reusable elements
- Document in corrections.md if post-launch fixes needed
- Complete results.md regardless of outcome

## Security Considerations

- Never commit API keys or credentials
- Sanitize any PII in documentation
- Use `.gitignore` for sensitive files
- Keep client-specific data in separate private repos

## Performance Impact

- All experiment code should be under 10KB minified
- Use async/defer for script loading
- Implement progressive enhancement
- Monitor Core Web Vitals impact

## Troubleshooting Guide

### Common Issues

1. **Selector Not Found**
   - Check docs/selectors.json for alternatives
   - Verify async load timing in architecture.md
   - Implement waitForElement utility

2. **Style Conflicts**
   - Check style-tokens.json for z-index values
   - Review fixes.json for similar issues
   - Use more specific selectors or !important

3. **JavaScript Errors**
   - Verify element exists before manipulation
   - Check gotchas.md for timing issues
   - Implement try-catch blocks

## Conclusion

This structure enables:
- **Rapid onboarding** for new developers and AI assistants
- **Consistent quality** across all experiments
- **Knowledge preservation** from every experiment
- **Reduced debugging time** through documented solutions
- **AI-powered development** with context-aware code generation

The system is designed to scale across unlimited clients while maintaining consistency and quality.
