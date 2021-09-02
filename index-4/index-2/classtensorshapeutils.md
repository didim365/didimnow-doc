# class tensorflow::TensorShapeUtils

Static helper routines for `TensorShape`. Includes a few common predicates on a tensor shape.

## Member Details

### `static bool tensorflow::TensorShapeUtils::IsScalar(const TensorShape &shape)` <a id="static_bool_tensorflow_TensorShapeUtils_IsScalar"></a>

### `static bool tensorflow::TensorShapeUtils::IsVector(const TensorShape &shape)` <a id="static_bool_tensorflow_TensorShapeUtils_IsVector"></a>

### `static bool tensorflow::TensorShapeUtils::IsVectorOrHigher(const TensorShape &shape)` <a id="static_bool_tensorflow_TensorShapeUtils_IsVectorOrHigher"></a>

### `static bool tensorflow::TensorShapeUtils::IsMatrix(const TensorShape &shape)` <a id="static_bool_tensorflow_TensorShapeUtils_IsMatrix"></a>

### `static bool tensorflow::TensorShapeUtils::IsMatrixOrHigher(const TensorShape &shape)` <a id="static_bool_tensorflow_TensorShapeUtils_IsMatrixOrHigher"></a>

### `static Status tensorflow::TensorShapeUtils::MakeShape(const int32 *dims, int n, TensorShape *out)` <a id="static_Status_tensorflow_TensorShapeUtils_MakeShape"></a>

Returns a `TensorShape` whose dimensions are `dims[0]`, `dims[1]`, ..., `dims[n-1]`.

### `static Status tensorflow::TensorShapeUtils::MakeShape(const int64 *dims, int n, TensorShape *out)` <a id="static_Status_tensorflow_TensorShapeUtils_MakeShape"></a>

### `string tensorflow::TensorShapeUtils::ShapeListString(const gtl::ArraySlice< TensorShape > &shapes)` <a id="string_tensorflow_TensorShapeUtils_ShapeListString"></a>

### `bool tensorflow::TensorShapeUtils::StartsWith(const TensorShape &shape0, const TensorShape &shape1)` <a id="bool_tensorflow_TensorShapeUtils_StartsWith"></a>

