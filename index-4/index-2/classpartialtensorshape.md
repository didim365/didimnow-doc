# class tensorflow::PartialTensorShape

Manages the partially known dimensions of a Tensor and their sizes.

## Member Details

### `tensorflow::PartialTensorShape::PartialTensorShape()` <a id="tensorflow_PartialTensorShape_PartialTensorShape"></a>

Construct an unknown `PartialTensorShape`.

### `tensorflow::PartialTensorShape::PartialTensorShape(gtl::ArraySlice< int64 > dim_sizes)` <a id="tensorflow_PartialTensorShape_PartialTensorShape"></a>

Construct a `PartialTensorShape` from the provided sizes. REQUIRES: `dim_sizes[i] >= 0`

### `tensorflow::PartialTensorShape::PartialTensorShape(std::initializer_list< int64 > dim_sizes)` <a id="tensorflow_PartialTensorShape_PartialTensorShape"></a>

### `tensorflow::PartialTensorShape::PartialTensorShape(const TensorShapeProto &proto)` <a id="tensorflow_PartialTensorShape_PartialTensorShape"></a>

REQUIRES: `IsValid(proto)`

### `PartialTensorShape tensorflow::PartialTensorShape::Concatenate(int64 size) const` <a id="PartialTensorShape_tensorflow_PartialTensorShape_Concatenate"></a>

Add a dimension to the end \("inner-most"\), returns a new PartialTensorShape . REQUIRES: `size >= -1`, where -1 means unknown

### `PartialTensorShape tensorflow::PartialTensorShape::Concatenate(const PartialTensorShape &shape) const` <a id="PartialTensorShape_tensorflow_PartialTensorShape_Concatenate"></a>

Appends all the dimensions from `shape`. Returns a new PartialTensorShape .

### `Status tensorflow::PartialTensorShape::MergeWith(const PartialTensorShape &shape, PartialTensorShape *result) const` <a id="Status_tensorflow_PartialTensorShape_MergeWith"></a>

Merges all the dimensions from `shape`. Returns `InvalidArgument` error if either `shape` has a different rank or if any of the dimensions are incompatible.

### `int tensorflow::PartialTensorShape::dims() const` <a id="int_tensorflow_PartialTensorShape_dims"></a>

Return the number of dimensions in the tensor. If the number of dimensions is unknown, return -1.

### `bool tensorflow::PartialTensorShape::IsFullyDefined() const` <a id="bool_tensorflow_PartialTensorShape_IsFullyDefined"></a>

Return true iff the rank and all of the dimensions are well defined.

### `bool tensorflow::PartialTensorShape::IsCompatibleWith(const PartialTensorShape &shape) const` <a id="bool_tensorflow_PartialTensorShape_IsCompatibleWith"></a>

Return true iff the ranks match, and if the dimensions all either match or one is unknown.

### `bool tensorflow::PartialTensorShape::IsCompatibleWith(const TensorShape &shape) const` <a id="bool_tensorflow_PartialTensorShape_IsCompatibleWith"></a>

Return true iff the dimensions of `shape` are compatible with `*this`.

### `int64 tensorflow::PartialTensorShape::dim_size(int d) const` <a id="int64_tensorflow_PartialTensorShape_dim_size"></a>

Returns the number of elements in dimension `d`. REQUIRES: `0 <= d < dims()`

### `gtl::ArraySlice<int64> tensorflow::PartialTensorShape::dim_sizes() const` <a id="gtl_ArraySlice_int64_tensorflow_PartialTensorShape_dim_sizes"></a>

Returns sizes of all dimensions.

### `void tensorflow::PartialTensorShape::AsProto(TensorShapeProto *proto) const` <a id="void_tensorflow_PartialTensorShape_AsProto"></a>

Fill `*proto` from `*this`.

### `bool tensorflow::PartialTensorShape::AsTensorShape(TensorShape *tensor_shape) const` <a id="bool_tensorflow_PartialTensorShape_AsTensorShape"></a>

### `string tensorflow::PartialTensorShape::DebugString() const` <a id="string_tensorflow_PartialTensorShape_DebugString"></a>

For error messages.

### `bool tensorflow::PartialTensorShape::IsValid(const TensorShapeProto &proto)` <a id="bool_tensorflow_PartialTensorShape_IsValid"></a>

Returns `true` iff `proto` is a valid partial tensor shape.

### `Status tensorflow::PartialTensorShape::IsValidShape(const TensorShapeProto &proto)` <a id="Status_tensorflow_PartialTensorShape_IsValidShape"></a>

Returns `OK` iff `proto` is a valid tensor shape, and a descriptive error status otherwise.

### `string tensorflow::PartialTensorShape::DebugString(const TensorShapeProto &proto)` <a id="string_tensorflow_PartialTensorShape_DebugString"></a>

### `static Status tensorflow::PartialTensorShape::MakePartialShape(const int32 *dims, int n, PartialTensorShape *out)` <a id="static_Status_tensorflow_PartialTensorShape_MakePartialShape"></a>

Returns a `PartialTensorShape` whose dimensions are `dims[0]`, `dims[1]`, ..., `dims[n-1]`. Values of -1 are considered "unknown".

### `static Status tensorflow::PartialTensorShape::MakePartialShape(const int64 *dims, int n, PartialTensorShape *out)` <a id="static_Status_tensorflow_PartialTensorShape_MakePartialShape"></a>

