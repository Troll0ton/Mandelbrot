# Mandelbrot
using AVX-instructions on the example of drawing a fractal
This project is aimed at analysing the applications of **AVX-instructions** in working with graphics, on the example of drawing Mandelbrot.

![alt-текст][mandelbrot]

[mandelbrot]: https://github.com/Troll0ton/Mandelbrot/blob/main/mandelbrot.png

---

## SSE-instructions and it's usage
I used **SSE-instructions** that allowed 4 colors to be packed into one 128-bit register, and vector transformations and calculations were already performed on it, instead of 4 different calculations.

```
        __m128i front_vector_l = _mm_load_si128 ((__m128i*)((uint32_t*) (&front_image_info.raster[CURR_POS])));
        __m128i back_vector_l  = _mm_load_si128 ((__m128i*)((uint32_t*) (&back_image_info.raster[CURR_POS])));

```


Since my project is aimed at studying SSE instructions, a necessary component of it was to compare the speeds of the program with and without their using.
To avoid the impact of using the SFML library, each pixel was calculated 500 times. 
```
        for(int i = 0; i < N(TESTS); i++)                   // Blending
        {                                                   //
            alpha_blending_fast (&res_image_info,           //
                                  table_image_info,         //
                                  cat_image_info   );       //
        } 
```
Also, in my project, optimization of only the second level (**-02**) was used.
This allowed the compiler to avoid using optimizations related to the topic of my project. The programmer needs to check the correctness of the application of SIMD instructions
so that the effect of the application is most noticeable in the speed of the program.


---

## Results
When making comparisons, the results of which are given below, it turned out to speed up the work of the program a **3 time**s.

| Vers.  |  IPS   |
| ------ | ------ |
| NO SSE |  1.37  | 
| SSE    |  4.05  |


---


## Conclusion
As a result, I would like to note that the use of SIMD instructions is one of the effective methods of optimizing the operation of the program.
The performance advantage is achieved when it is necessary to perform the same sequence of actions on different data.
In this case, the SIMD block parallelizes the computational process between the data.
This project also includes work with BMP format, its structure.
