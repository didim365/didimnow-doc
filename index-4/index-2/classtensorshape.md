# class tensorflow::TensorShape

## Member Details

### `uint8 tensorflow::TensorShape::buf[16][16]` <a id="uint8_tensorflow_TensorShape_buf_16_"></a>

### `Rep64* tensorflow::TensorShape::unused_aligner` <a id="Rep64_tensorflow_TensorShape_unused_aligner"></a>

### `tensorflow::TensorShape::TensorShape(gtl::ArraySlice< int64 > dim_sizes)` <a id="tensorflow_TensorShape_TensorShape"></a>

Construct a `TensorShape` from the provided sizes. REQUIRES: `dim_sizes[i] >= 0`

### `tensorflow::TensorShape::TensorShape(std::initializer_list< int64 > dim_sizes)` <a id="tensorflow_TensorShape_TensorShape"></a>

### `tensorflow::TensorShape::TensorShape(const TensorShapeProto &proto)` <a id="tensorflow_TensorShape_TensorShape"></a>

REQUIRES: `IsValid(proto)`

### `tensorflow::TensorShape::TensorShape()` <a id="tensorflow_TensorShape_TensorShape"></a>

Create a tensor shape with no dimensions and one element, which you can then call `AddDim()` on.

### `tensorflow::TensorShape::~TensorShape()` <a id="tensorflow_TensorShape_TensorShape"></a>

### `tensorflow::TensorShape::TensorShape(const TensorShape &b)` <a id="tensorflow_TensorShape_TensorShape"></a>

Copy the specified shape.

### `void tensorflow::TensorShape::operator=(const TensorShape &b)` <a id="void_tensorflow_TensorShape_operator_"></a>

### `void tensorflow::TensorShape::Clear()` <a id="void_tensorflow_TensorShape_Clear"></a>

Clear a tensor shape.

### `void tensorflow::TensorShape::AddDim(int64 size)` <a id="void_tensorflow_TensorShape_AddDim"></a>

Add a dimension to the end \("inner-most"\). REQUIRES: `size >= 0`

### `void tensorflow::TensorShape::AppendShape(const TensorShape &shape)` <a id="void_tensorflow_TensorShape_AppendShape"></a>

Appends all the dimensions from `shape`.

### `void tensorflow::TensorShape::InsertDim(int d, int64 size)` <a id="void_tensorflow_TensorShape_InsertDim"></a>

Insert a dimension somewhere in the `TensorShape`. REQUIRES: `0 <= d <= dims()` REQUIRES: `size >= 0`

### `void tensorflow::TensorShape::set_dim(int d, int64 size)` <a id="void_tensorflow_TensorShape_set_dim"></a>

Modifies the size of the dimension `d` to be `size` REQUIRES: `0 <= d < dims()` REQUIRES: `size >= 0`

### `void tensorflow::TensorShape::RemoveDim(int d)` <a id="void_tensorflow_TensorShape_RemoveDim"></a>

Removes dimension `d` from the `TensorShape`. REQUIRES: `0 <= d < dims()`

### `int tensorflow::TensorShape::dims() const` <a id="int_tensorflow_TensorShape_dims"></a>

Return the number of dimensions in the tensor.

### `int64 tensorflow::TensorShape::dim_size(int d) const` <a id="int64_tensorflow_TensorShape_dim_size"></a>

Returns the number of elements in dimension `d`. REQUIRES: `0 <= d < dims()`

### `gtl::InlinedVector< int64, 4 > tensorflow::TensorShape::dim_sizes() const` <a id="gtl_InlinedVector_int64_4_tensorflow_TensorShape_dim_sizes"></a>

Returns sizes of all dimensions.

### `int64 tensorflow::TensorShape::num_elements() const` <a id="int64_tensorflow_TensorShape_num_elements"></a>

Returns the number of elements in the tensor.

We use `int64` and not `size_t` to be compatible with `Eigen::Tensor` which uses `ptrdiff_t`.

### `bool tensorflow::TensorShape::IsSameSize(const TensorShape &b) const` <a id="bool_tensorflow_TensorShape_IsSameSize"></a>

Returns true if `*this` and `b` have the same sizes. Ignores dimension names.

### `bool tensorflow::TensorShape::operator==(const TensorShape &b) const` <a id="bool_tensorflow_TensorShape_operator_"></a>

### `bool tensorflow::TensorShape::operator!=(const TensorShape &b) const` <a id="bool_tensorflow_TensorShape_operator_"></a>

### `void tensorflow::TensorShape::AsProto(TensorShapeProto *proto) const` <a id="void_tensorflow_TensorShape_AsProto"></a>

Fill `*proto` from `*this`.

### `Eigen::DSizes< Eigen::DenseIndex, NDIMS > tensorflow::TensorShape::AsEigenDSizes() const` <a id="Eigen_DSizes_Eigen_DenseIndex_NDIMS_tensorflow_TensorShape_AsEigenDSizes"></a>

Fill `*dsizes` from `*this`.

### `Eigen::DSizes< Eigen::DenseIndex, NDIMS > tensorflow::TensorShape::AsEigenDSizesWithPadding() const` <a id="Eigen_DSizes_Eigen_DenseIndex_NDIMS_tensorflow_TensorShape_AsEigenDSizesWithPadding"></a>

Same as `AsEigenDSizes()` but allows for `NDIMS > dims()` in which case we pad the rest of the sizes with 1.

### `TensorShapeIter tensorflow::TensorShape::begin() const` <a id="TensorShapeIter_tensorflow_TensorShape_begin"></a>

For iterating through the dimensions.

### `TensorShapeIter tensorflow::TensorShape::end() const` <a id="TensorShapeIter_tensorflow_TensorShape_end"></a>

### `string tensorflow::TensorShape::DebugString() const` <a id="string_tensorflow_TensorShape_DebugString"></a>

For error messages.

### `void tensorflow::TensorShape::DumpRep() const` <a id="void_tensorflow_TensorShape_DumpRep"></a>

### `bool tensorflow::TensorShape::IsValid(const TensorShapeProto &proto)` <a id="bool_tensorflow_TensorShape_IsValid"></a>

Returns `true` iff `proto` is a valid tensor shape.

### `Status tensorflow::TensorShape::IsValidShape(const TensorShapeProto &proto)` <a id="Status_tensorflow_TensorShape_IsValidShape"></a>

Returns `OK` iff `proto` is a valid tensor shape, and a descriptive error status otherwise.

### `static constexpr int tensorflow::TensorShape::MaxDimensions()` <a id="static_constexpr_int_tensorflow_TensorShape_MaxDimensions"></a>

### `string tensorflow::TensorShape::DebugString(const TensorShapeProto &proto)` <a id="string_tensorflow_TensorShape_DebugString"></a>

Same as `TensorShape(proto). DebugString()` but doesn't crash for invalid protos.

