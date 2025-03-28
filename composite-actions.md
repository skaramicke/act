# Composite Actions Support Implementation Plan

## Overview
This document outlines the plan for implementing GitHub Composite Actions support in act. Composite actions allow users to combine multiple workflow steps into a reusable action, which can then be used in other workflows.

## 1. Testing Strategy

### Test Cases
1. **Basic Composite Action Tests**
   - Test parsing of composite action metadata (action.yml)
   - Test basic step execution within composite actions
   - Test input/output handling between composite and calling workflow

2. **Complex Scenarios**
   - Nested composite actions (composite actions calling other composite actions)
   - Composite actions with conditional steps
   - Composite actions with environment variables
   - Composite actions with secrets handling

3. **Edge Cases**
   - Error handling in composite actions
   - Timeout scenarios
   - Resource cleanup
   - Invalid composite action definitions

### Testing Infrastructure
1. **Test Workflows**
   - Create a dedicated test repository with sample composite actions
   - Implement GitHub Actions workflows that use these composite actions
   - Create corresponding act-compatible test cases

2. **Integration Tests**
   - Add test cases to act's existing test suite
   - Create new test files specifically for composite actions
   - Implement test helpers for composite action validation

3. **Validation Tools**
   - Create tools to validate composite action definitions
   - Implement schema validation for action.yml files
   - Add runtime validation for composite action execution

## 2. MVP Implementation

### Phase 1: Basic Support
1. **Parser Updates**
   - Extend action parser to handle composite action metadata
   - Add support for parsing composite action steps
   - Implement input/output mapping

2. **Runtime Support**
   - Add composite action execution engine
   - Implement step execution within composite actions
   - Handle environment variable scoping

3. **Integration**
   - Update workflow runner to detect and handle composite actions
   - Implement composite action resolution
   - Add basic error handling

### Phase 2: Enhanced Features
1. **Advanced Features**
   - Support for nested composite actions
   - Conditional step execution
   - Environment variable inheritance
   - Secrets handling

2. **Performance Optimization**
   - Caching of composite action definitions
   - Optimized step execution
   - Resource management

## 3. Code Standards

### Style Guidelines
1. **Code Organization**
   - Follow existing act codebase structure
   - Maintain consistent package organization
   - Use clear and descriptive naming conventions

2. **Documentation**
   - Add inline documentation for new functions
   - Update existing documentation
   - Include examples in comments

3. **Testing**
   - Maintain test coverage requirements
   - Follow existing test patterns
   - Include both unit and integration tests

### Quality Checks
1. **Code Review Process**
   - Ensure all new code follows act's style guide
   - Verify test coverage
   - Check for proper error handling

2. **Performance Considerations**
   - Monitor execution time
   - Optimize resource usage
   - Consider caching strategies

## 4. Documentation Updates

### Technical Documentation
1. **Code Documentation**
   - Update API documentation
   - Add composite action examples
   - Document new configuration options

2. **User Documentation**
   - Create composite action usage guide
   - Add troubleshooting section
   - Include best practices

### Integration Guide
1. **Usage Examples**
   - Basic composite action creation
   - Advanced usage scenarios
   - Common patterns and anti-patterns

2. **Configuration**
   - Document new configuration options
   - Explain environment setup
   - Provide troubleshooting steps

## Timeline and Milestones

1. **Week 1-2: Testing Infrastructure**
   - Set up test environment
   - Create initial test cases
   - Implement validation tools

2. **Week 3-4: MVP Development**
   - Implement basic composite action support
   - Add core functionality
   - Create initial integration tests

3. **Week 5-6: Enhancement and Refinement**
   - Add advanced features
   - Optimize performance
   - Improve error handling

4. **Week 7-8: Documentation and Review**
   - Update documentation
   - Perform code review
   - Final testing and validation

## Success Criteria

1. **Functionality**
   - All test cases pass
   - Composite actions work as expected
   - Performance meets requirements

2. **Code Quality**
   - Follows act's coding standards
   - Maintains test coverage
   - Properly documented

3. **User Experience**
   - Clear documentation
   - Intuitive usage
   - Helpful error messages

## Next Steps

1. Review and approve implementation plan
2. Set up development environment
3. Begin testing infrastructure implementation
4. Start MVP development 

## Todo List

### Phase 1: Testing Infrastructure
- [ ] Create test repository structure
  - [ ] Set up `pkg/runner/testdata/composite-actions/` directory
  - [ ] Create sample composite action definitions
  - [ ] Create test workflows using composite actions
- [ ] Implement test framework
  - [ ] Create `pkg/runner/composite_action_test.go` for unit tests
  - [ ] Add mock implementations for composite action execution
  - [ ] Set up test helpers for composite action validation
- [ ] Write test cases
  - [ ] Basic composite action parsing tests
  - [ ] Step execution within composite actions
  - [ ] Input/output handling tests
  - [ ] Environment variable scoping tests
  - [ ] Error handling tests
- [ ] Integration tests
  - [ ] Add composite action test workflows to CI
  - [ ] Create end-to-end test scenarios
  - [ ] Test composite action caching
- [ ] Validation tools
  - [ ] Implement action.yml schema validation
  - [ ] Add runtime validation for composite actions
  - [ ] Create test utilities for composite action validation

### Phase 2: MVP Development
- [ ] Extend action parser for composite actions
- [ ] Implement composite action metadata handling
- [ ] Add basic step execution within composites
- [ ] Implement input/output mapping
- [ ] Add environment variable scoping
- [ ] Create composite action resolution system
- [ ] Implement basic error handling

### Phase 3: Enhanced Features
- [ ] Add support for nested composite actions
- [ ] Implement conditional step execution
- [ ] Add environment variable inheritance
- [ ] Implement secrets handling
- [ ] Add caching for composite actions
- [ ] Optimize step execution
- [ ] Implement resource management

### Phase 4: Documentation and Review
- [ ] Update API documentation
- [ ] Create user guide for composite actions
- [ ] Add troubleshooting section
- [ ] Write usage examples
- [ ] Document configuration options
- [ ] Perform code review
- [ ] Final testing and validation

### Ongoing Tasks
- [ ] Maintain test coverage
- [ ] Follow code style guidelines
- [ ] Update documentation as features are added
- [ ] Review and optimize performance
- [ ] Address user feedback 