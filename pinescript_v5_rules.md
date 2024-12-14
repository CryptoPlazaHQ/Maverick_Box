# 📜 Pine Script v5 Development Rules & Changes

## 🆕 Major Changes from Previous Versions

### 1. 🏗️ Type System
- Introduction of User-Defined Types (UDT)
- Strict type checking
- Type declarations required for custom types
```pinescript
type MyType
    int field1
    float field2
    bool field3
```

### 2. 📦 Object-Oriented Features
- Method-like syntax for UDTs
- Constructors using Type.new()
- Better encapsulation of related data
```pinescript
myObject = MyType.new(field1=1, field2=2.0, field3=true)
```

### 3. 🔄 Arrays and Data Structures
- Dynamic array operations
- Multi-dimensional arrays supported
- Array methods: push(), pop(), shift(), unshift()
- Maximum array size limit: 100,000 elements
```pinescript
var myArray = array.new<float>()
array.push(myArray, close)
```

### 4. ⚠️ Key Limitations

#### Memory Constraints
- Maximum variables per script: 1000
- Maximum array size: 100,000 elements
- Maximum string length: 500 characters
- Maximum function parameters: 64

#### Computational Constraints
- No recursive functions
- No while loops
- Limited nested for loops
- Maximum script runtime: ~500ms

#### Data Access Restrictions
- Can't access future data
- Limited historical data access
- No direct file I/O
- No external API calls

### 5. 🎯 ML-Specific Considerations

#### Supported
- Feature calculation
- Simple statistical operations
- Basic pattern recognition
- Signal generation
- Array-based calculations
- Custom indicators

#### Not Supported
- Direct model training
- Complex matrix operations
- Deep learning operations
- Model persistence
- Real-time model updates

### 6. 🔄 Request.security() Rules
- Must respect market hours
- No future data access
- Limited historical data
- Timeframe restrictions
```pinescript
request.security(syminfo.tickerid, timeframe.period, close)
```

### 7. 📊 Variable Scope Rules
- Global variables must use 'var' keyword
- Block scope within if/for statements
- No variable shadowing
```pinescript
var float globalVar = 0.0
if condition
    float localVar = 1.0  // only visible in this block
```

### 8. ⚡ Performance Optimization Rules
- Minimize array operations in loops
- Use var keyword for persistent variables
- Avoid unnecessary calculations
- Use built-in functions when possible
```pinescript
// Efficient
var calculations = array.new<float>()
// Less efficient
calculations = array.new<float>()  // recreated every bar
```

### 9. 🎨 Drawing Objects
- Maximum objects limits
  * Lines: 500
  * Labels: 500
  * Boxes: 500
- Auto-removal of old objects required
```pinescript
var boxArray = array.new<box>()
if array.size(boxArray) > 100
    box.delete(array.shift(boxArray))
```

### 10. 🔍 Error Handling
- No try-catch blocks
- Limited error checking
- Must handle errors through conditional logic
```pinescript
if na(close)
    // handle missing data
else
    // process data
```

## 🎯 Impact on Hybrid Implementation

### What's Possible in Pine Script v5
1. Feature extraction
2. Basic pattern recognition
3. Signal generation
4. Data preparation for external processing
5. Box formation detection
6. Volume analysis
7. Basic statistical calculations

### What Must Be Done Externally
1. Complex ML model training
2. Deep learning operations
3. Advanced pattern recognition
4. Model persistence
5. Complex matrix operations
6. Historical data analysis

## 📝 Best Practices for Our Implementation

1. 📊 Data Management
- Use arrays efficiently
- Implement cleanup routines
- Monitor memory usage
- Cache calculations where possible

2. 🔄 Performance
- Minimize per-bar calculations
- Use built-in functions
- Implement efficient data structures
- Avoid redundant calculations

3. 🎯 Signal Generation
- Clear entry/exit logic
- Robust error handling
- Efficient box detection
- Clean drawing object management

4. 📤 Data Export
- Format data efficiently
- Implement proper serialization
- Handle missing data
- Maintain data integrity

This understanding of Pine Script v5 rules and limitations will guide our hybrid implementation strategy, ensuring we leverage its strengths while avoiding its constraints through external processing where necessary.
