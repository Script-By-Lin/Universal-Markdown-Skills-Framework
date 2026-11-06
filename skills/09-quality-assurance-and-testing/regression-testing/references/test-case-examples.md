# Regression Test Case Examples & Templates (Level 3 Reference)
# Universal Markdown Skills Framework (UMSF)

> Version: 1.7.0  
> Authority: Level 3 Optional Reference Asset for `regression-testing`  
> Domain: 09 — Quality Assurance & Testing  

---

## 1. Overview
Concrete examples and templates for regression test cases, including defect-reproduction test patterns, snapshot regression tests, and backward-compatibility fixtures across TypeScript, Python, and Go.

---

## 2. Bug Reproduction Regression Test Patterns

### 2.1 Pattern: Defect Fix Permanence (TypeScript / Jest / Vitest)
```typescript
describe("Regression: Defect Fix Permanence", () => {
  // Always cite the issue or bug ID in the test title
  it("REG-BUG-1042: handles null payload gracefully without uncaught TypeError", async () => {
    // 1. Arrange: reconstruct the exact defect-triggering payload
    const malformedPayload = { userId: "user-123", metadata: null };
    
    // 2. Act: invoke the service function that previously threw
    const result = await processUserPayload(malformedPayload);
    
    // 3. Assert: verify graceful fallback handling
    expect(result.status).toBe("handled_with_defaults");
    expect(result.metadata).toEqual({});
  });
});
```

### 2.2 Pattern: Boundary Condition Regression (Python / Pytest)
```python
import pytest
from app.calculator import calculate_discount

@pytest.mark.regression
def test_reg_bug_882_zero_division_when_cart_empty():
    """Verify calculating discount on empty cart returns Decimal('0.00') instead of raising ZeroDivisionError."""
    result = calculate_discount(total_items=0, total_amount=0)
    assert result == 0.0
```

---

## 3. Snapshot & State Regression Templates
- Store baseline snapshot files in version control under `tests/__snapshots__/`.
- When updating snapshots, review line-by-line diffs to ensure intentional modifications only.
- Never run `--updateSnapshot` blindly across the entire test suite.

