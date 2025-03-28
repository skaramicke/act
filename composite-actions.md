# Composite Actions Secrets Support Improvement Plan

## Overview
This document outlines the plan for improving secrets handling in composite actions to match GitHub Actions' behavior. Currently, act strips secrets from composite actions, which prevents them from accessing secrets in the same way as GitHub Actions does.

## 1. Current State

### Existing Implementation
- Composite actions are supported in act
- Basic functionality works (steps, inputs, outputs, environment variables)
- Secrets are stripped from composite actions (`configCopy.Secrets = nil` in `action_composite.go`)
- Users must work around this by passing secrets as inputs

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

2. **Complex Scenarios**
   - Nested composite actions with secrets
   - Secrets in conditional steps
   - Secrets in output values
   - Secrets in environment variables

3. **Edge Cases**
   - Invalid secret references
   - Missing secrets
   - Secret masking
   - Secret scoping

### Testing Infrastructure
1. **Test Workflows**
   - Create test cases that mirror GitHub Actions behavior
   - Test both local and remote composite actions
   - Verify secret masking and security

2. **Integration Tests**
   - Add test cases to act's existing test suite
   - Create new test files for secrets handling
   - Implement test helpers for secret validation

## 3. Implementation Plan

### Phase 1: Core Changes
1. **Remove Secrets Stripping**
   - Remove `configCopy.Secrets = nil` in `action_composite.go`
   - Ensure secrets are properly passed to composite actions
   - Maintain existing security model

2. **Update Environment Handling**
   - Modify environment variable handling to include secrets
   - Ensure proper scoping of secrets
   - Handle secret masking

3. **Expression Evaluation**
   - Update expression evaluator to handle secrets in composite actions
   - Ensure proper interpolation of secret values
   - Handle secret references in outputs

### Phase 2: Enhanced Features
1. **Security Improvements**
   - Add secret validation
   - Implement proper secret scoping
   - Add secret masking in logs

2. **Performance Optimization**
   - Optimize secret handling
   - Cache secret values where appropriate
   - Minimize secret exposure

## 4. Code Standards

### Style Guidelines
1. **Code Organization**
   - Follow existing act codebase structure
   - Maintain consistent package organization
   - Use clear and descriptive naming conventions

2. **Documentation**
   - Add inline documentation for secret handling
   - Update existing documentation
   - Include security considerations

3. **Testing**
   - Maintain test coverage requirements
   - Follow existing test patterns
   - Include both unit and integration tests

### Quality Checks
1. **Security Review**
   - Ensure proper secret handling
   - Verify secret masking
   - Check for security vulnerabilities

2. **Performance Considerations**
   - Monitor secret handling overhead
   - Optimize secret access
   - Consider caching strategies

## 5. Documentation Updates

### Technical Documentation
1. **Code Documentation**
   - Update secret handling documentation
   - Add composite action secret examples
   - Document security considerations

2. **User Documentation**
   - Create secret handling guide
   - Add troubleshooting section
   - Include best practices

### Integration Guide
1. **Usage Examples**
   - Basic secret access in composite actions
   - Advanced secret handling scenarios
   - Security best practices

2. **Configuration**
   - Document secret configuration
   - Explain security setup
   - Provide troubleshooting steps

## Success Criteria

1. **Functionality**
   - Secrets work identically to GitHub Actions
   - All test cases pass
   - Performance meets requirements

2. **Security**
   - Proper secret handling
   - Secure secret access
   - No security vulnerabilities

3. **User Experience**
   - Clear documentation
   - Intuitive usage
   - Helpful error messages

## Next Steps

1. Begin implementation by removing secrets stripping in `action_composite.go`
2. Add test cases for secret handling
3. Update environment handling and expression evaluation
4. Implement security measures and secret masking
5. Update documentation

## Todo List

### Phase 1: Core Changes
- [ ] Remove secrets stripping
  - [ ] Update `action_composite.go`
  - [ ] Modify config handling
  - [ ] Update tests
- [ ] Update environment handling
  - [ ] Modify environment setup
  - [ ] Add secret support
  - [ ] Update tests
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
