cmake_minimum_required(VERSION 3.6)
project(rnnoise LANGUAGES C)

add_library(denoise STATIC
  src/celt_lpc.c
  src/kiss_fft.c
  src/pitch.c
  src/rnn.c
  src/rnn_data.c
)
include_directories(include)

add_executable(rnnoise_demo examples/rnnoise_demo.c src/denoise.c)
target_link_libraries(rnnoise_demo denoise -lm)

add_executable(denoise_training src/denoise.c)
target_link_libraries(denoise_training denoise -lm)
target_compile_definitions(denoise_training PRIVATE TRAINING=1)

