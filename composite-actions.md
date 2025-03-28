# Composite Actions Secrets Support Improvement Plan

## Overview
This document outlines the plan for improving secrets handling in composite actions to match GitHub Actions' behavior. Currently, act strips secrets from composite actions, which prevents them from accessing secrets in the same way as GitHub Actions does.

## 1. Current State

### Existing Implementation
- Composite actions are supported in act
- Basic functionality works (steps, inputs, outputs, environment variables)
- Secrets are stripped from composite actions (`configCopy.Secrets = nil` in `action_composite.go`)
- Users must work around this by passing secrets as inputs

### Historical Context
The original implementation stripped secrets from composite actions for several reasons:
1. **Conservative Security Approach**
   - Initial implementation took a conservative stance on security
   - Stripping secrets was a defensive measure during early development
   - This approach is overly restrictive compared to GitHub Actions

2. **Environment Variable Handling**
   - Complex environment setup in composite actions
   - Comment in code indicates environment handling complexity: "compositeRC.Env is dirty, contains INPUT_ and merged step env"
   - Secrets stripping was likely a workaround for environment variable conflicts

3. **Expression Evaluation**
   - Designed to prevent accidental secret exposure through expression evaluation
   - Current implementation is overly restrictive
   - GitHub Actions allows proper secret access in expressions

4. **Test Coverage**
   - Limited test coverage for secret handling in composite actions
   - No comprehensive tests for secret access patterns
   - Conservative approach due to lack of test coverage

### GitHub Actions Behavior
- Composite actions can access secrets directly using `${{ secrets.SECRET_NAME }}`
- Secrets are properly scoped and available in all steps
- No need to pass secrets as inputs
- Maintains security by only exposing secrets to authorized actions

## 2. Testing Strategy

### Test Cases
1. **Basic Secrets Access**
   - Test direct secrets access in composite actions
   - Verify secrets are available in all steps
   - Test secrets in environment variables
   - Validate secret access matches GitHub Actions behavior

2. **Complex Scenarios**
   - Nested composite actions with secrets
   - Secrets in conditional steps
   - Secrets in output values
   - Secrets in environment variables
   - Environment variable conflicts with secrets

3. **Edge Cases**
   - Invalid secret references
   - Missing secrets
   - Secret masking
   - Secret scoping
   - Expression evaluation with secrets

### Testing Infrastructure
1. **Test Workflows**
   - Create test cases that mirror GitHub Actions behavior
   - Test both local and remote composite actions
   - Verify secret masking and security
   - Test environment variable handling

2. **Integration Tests**
   - Add test cases to act's existing test suite
   - Create new test files for secrets handling
   - Implement test helpers for secret validation
   - Add tests for expression evaluation

## 3. Implementation Plan

### Phase 1: Core Changes
1. **Remove Secrets Stripping**
   - Remove `configCopy.Secrets = nil` in `action_composite.go`
   - Ensure secrets are properly passed to composite actions
   - Maintain existing security model
   - Add comprehensive test coverage first

2. **Update Environment Handling**
   - Modify environment variable handling to include secrets
   - Ensure proper scoping of secrets
   - Handle secret masking
   - Fix environment variable conflicts

3. **Expression Evaluation**
   - Update expression evaluator to handle secrets in composite actions
   - Ensure proper interpolation of secret values
   - Handle secret references in outputs
   - Add tests for expression evaluation

### Phase 2: Enhanced Features
1. **Security Improvements**
   - Add secret validation
   - Implement proper secret scoping
   - Add secret masking in logs
   - Ensure no accidental secret exposure

2. **Performance Optimization**
   - Optimize secret handling
   - Cache secret values where appropriate
   - Minimize secret exposure
   - Monitor environment variable performance

## 4. Code Standards

### Style Guidelines
1. **Code Organization**
   - Follow existing act codebase structure
   - Maintain consistent package organization
   - Use clear and descriptive naming conventions
   - Document security considerations

2. **Documentation**
   - Add inline documentation for secret handling
   - Update existing documentation
   - Include security considerations
   - Document environment variable behavior

3. **Testing**
   - Maintain test coverage requirements
   - Follow existing test patterns
   - Include both unit and integration tests
   - Add security-focused test cases

### Quality Checks
1. **Security Review**
   - Ensure proper secret handling
   - Verify secret masking
   - Check for security vulnerabilities
   - Validate environment variable security

2. **Performance Considerations**
   - Monitor secret handling overhead
   - Optimize secret access
   - Consider caching strategies
   - Monitor environment variable performance

## 5. Documentation Updates

### Technical Documentation
1. **Code Documentation**
   - Update secret handling documentation
   - Add composite action secret examples
   - Document security considerations
   - Document environment variable behavior

2. **User Documentation**
   - Create secret handling guide
   - Add troubleshooting section
   - Include best practices
   - Document environment variable usage

### Integration Guide
1. **Usage Examples**
   - Basic secret access in composite actions
   - Advanced secret handling scenarios
   - Security best practices
   - Environment variable examples

2. **Configuration**
   - Document secret configuration
   - Explain security setup
   - Provide troubleshooting steps
   - Document environment variable setup

## Success Criteria

1. **Functionality**
   - Secrets work identically to GitHub Actions
   - All test cases pass
   - Performance meets requirements
   - Environment variables work correctly

2. **Security**
   - Proper secret handling
   - Secure secret access
   - No security vulnerabilities
   - No accidental secret exposure

3. **User Experience**
   - Clear documentation
   - Intuitive usage
   - Helpful error messages
   - Consistent with GitHub Actions

## Next Steps

1. Add comprehensive test cases for secret handling
2. Remove secrets stripping in `action_composite.go`
3. Update environment handling and expression evaluation
4. Implement security measures and secret masking
5. Update documentation

## Todo List

### Phase 1: Core Changes
- [ ] Add test cases
  - [ ] Basic secret access tests
  - [ ] Environment variable tests
  - [ ] Expression evaluation tests
- [ ] Remove secrets stripping
  - [ ] Update `action_composite.go`
  - [ ] Modify config handling
  - [ ] Update tests
- [ ] Update environment handling
  - [ ] Modify environment setup
  - [ ] Add secret support
  - [ ] Fix environment conflicts
- [ ] Update expression evaluation
  - [ ] Modify expression evaluator
  - [ ] Add secret interpolation
  - [ ] Update tests

### Phase 2: Security and Testing
- [ ] Add security measures
  - [ ] Implement secret validation
  - [ ] Add secret scoping
  - [ ] Implement secret masking
- [ ] Add test cases
  - [ ] Basic secret access tests
  - [ ] Complex scenario tests
  - [ ] Edge case tests
- [ ] Performance optimization
  - [ ] Optimize secret handling
  - [ ] Add caching where appropriate
  - [ ] Minimize secret exposure

### Phase 3: Documentation
- [ ] Update technical documentation
  - [ ] Document secret handling
  - [ ] Add code examples
  - [ ] Update API docs
- [ ] Create user documentation
  - [ ] Write usage guide
  - [ ] Add troubleshooting
  - [ ] Include best practices
- [ ] Security documentation
  - [ ] Document security model
  - [ ] Add security guidelines
  - [ ] Include security considerations

### Ongoing Tasks
- [ ] Maintain test coverage
- [ ] Follow code style guidelines
- [ ] Update documentation
- [ ] Review security
- [ ] Address user feedback
