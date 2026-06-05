### match
```cpp
...
 namespace 
 dino_image 
 { 
 >>> 
// Width of the dino pixel data.
 ... } ...  
```
### patch
```cpp
// Width of the lion pixel data.
static constexpr int kDinoWidth = 22;
// Height of the lion pixel data.
static constexpr int kDinoHeight = 24;
// Height of the lion pixel data, top segment.
static constexpr int kDinoHeadHeight = 1;
// Height of the lion image data, body segment.
static constexpr int kDinoBodyHeight = kDinoHeight - kDinoHeadHeight;
// Width of the lion image data.
static constexpr int kDinoWidthBytes = (kDinoWidth + 7) / 8;
// Pixel data for the lion's head (original lion)
static const unsigned char kDinoHeadRight[kDinoWidthBytes * kDinoHeadHeight] = {
    // clang-format off
  0b00000000, 0b11111100, 0b00000000,
    // clang-format on
};

// Pixel data for the lion's head (original lion, maybe add sunglasses later?)
static const unsigned char kDinoHeadLeft[kDinoWidthBytes * kDinoHeadHeight] = {
    // clang-format off
  0b00000000, 0b11111100, 0b00000000,
    // clang-format on
};

// Pixel data for the lion's body.
static const unsigned char kDinoBody[kDinoWidthBytes * kDinoBodyHeight] = {
    // clang-format off
  0b00000011, 0b11111111, 0b00000000,
  0b00011111, 0b11111111, 0b11100000,
  0b00111111, 0b11111111, 0b11110000,
  0b01111000, 0b00000000, 0b01111000,
  0b00110000, 0b00000000, 0b00110000,
  0b01110011, 0b11001111, 0b00111000,
  0b01100000, 0b11001100, 0b00011000,
  0b01100000, 0b10000100, 0b00011000,
  0b01110000, 0b00000000, 0b00111000,
  0b00111000, 0b11001100, 0b01110000,
  0b00111100, 0b01111000, 0b11110000,
  0b00011100, 0b00110000, 0b11100000,
  0b00011000, 0b00110000, 0b01100000,
  0b00011100, 0b01111000, 0b11100000,
  0b00011111, 0b10000111, 0b11100000,
  0b00001111, 0b00000011, 0b11000000,
  0b00001111, 0b10000111, 0b11000000,
  0b00001111, 0b11001111, 0b11000000,
  0b00000111, 0b11111111, 0b10000000,
  0b00000011, 0b11111111, 0b00000000,
  0b00000001, 0b11111110, 0b00000000,
  0b00000000, 0b01111000, 0b00000000,
  0b00000000, 0b00110000, 0b00000000,
    // clang-format on
};

```

