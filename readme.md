# Wavefront OBJ parser in C

Wavefront .OBJ files parser in C.

## How to build

```sh
git clone https://github.com/silentstranger5/obj
cd obj
cmake -B build -S .
cmake --build build
```

## How to use

```c
#include <obj.h>
#include <stdio.h>

int main(int argc, char **argv)
{
    obj_ctx octx;
    objctx_init(&octx);
    int ok = parse_obj("file.obj");
    if (!ok)
    {
        printf("file.obj does not exist\n");
        return 1;
    }
    int idx = lookup(&octx, "object");
    if (idx < 0)
    {
        printf("object data not found\n");
        return 1;
    }
    model *mod = array_get(&octx.models, idx);
    if (!mod)
    {
        printf("object model not found\n");
        return 1;
    }
    material *mtl = array_get(&octx.materials, idx);
    if (!mtl)
    {
        printf("object material not found\n");
        return 1;
    }
    objctx_free(&octx);
    return 0;
}
```

## About

This is a Wavefront .obj parser written in C. 
For simplicity of implementation, format of input files is very restricted.

- each vertex must contain position, normal and texture coordinate
- each face must contain exactly three vertices
- length of strings used in names of models, materials or textures, must not exceed 32 characters
- this library only parses information; locating and loading textures in memory is user's responsibility
