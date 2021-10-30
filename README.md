[![crates.io](https://img.shields.io/crates/v/libstacker.svg)](https://crates.io/crates/libstacker)
[![Documentation](https://docs.rs/libstacker/badge.svg)](https://docs.rs/libstacker)
[![Workflow](https://github.com/eadf/libstacker.rs/workflows/Rust/badge.svg)](https://github.com/eadf/libstacker.rs/workflows/Rust/badge.svg)
[![dependency status](https://deps.rs/crate/libstacker/0.0.1/status.svg)](https://deps.rs/crate/libstacker/0.0.1)
![license](https://img.shields.io/crates/l/libstacker)

# libstacker
A multi-threaded port of the python code found [here: github.com/maitek/image_stacking](https://github.com/maitek/image_stacking) 

## Usage:
### Download the test images:

```git clone https://github.com/maitek/image_stacking image_stacking_py```

### Build the code:
Opencv-rust can be little tricky to install. Follow the instructions from [rust opencv](https://crates.io/crates/opencv)

```cargo build --release```

### Run the example:

```cargo run --example main --release```

and then wait a few seconds. The result should be two windows showing the stacked images.

## API
```rust
let keypoint_match_img:opencv::Mat = keypoint_match(
   // a Vec<PathBuf> containing paths to image files
   collect_image_files(&PathBuf::from("image_stacking_py/images"))?,
   KeyPointMatchParameters {
      method: opencv::calib3d::RANSAC,
      ransac_reproj_threshold: 5.0,
   },
)?;
```

Depending on the parameters the `ecc_match()` is much slower, but also more accurate. 
```rust
let ecc_match_img:opencv::Mat = ecc_match(
   // a Vec<PathBuf> containing paths to image files
   collect_image_files(&PathBuf::from("image_stacking_py/images"))?,
   EccMatchParameters {
      max_count: Some(5000),
      epsilon: Some(1e-5),
      gauss_filt_size: 5,
   },
)?;
```

## Todo

* Figure out what to do with `.reshape()` in `keypoint_match()`
* ~~Figure out some opencv parameters~~ responsibility shifted to end user.
* Command line options in the example

## License

Licensed under either of

* Apache License, Version 2.0, ([LICENSE-APACHE](LICENSE-APACHE) or <http://www.apache.org/licenses/LICENSE-2.0)>
* MIT license ([LICENSE-MIT](LICENSE-MIT) or <http://opensource.org/licenses/MIT)>

at your option.
