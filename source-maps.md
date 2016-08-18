# [JavaScript Source Maps](http://www.html5rocks.com/en/tutorials/developertools/sourcemaps/)

Basically it's a way to map a combined/minified file back to an unbuilt state. When building for production, and minifying and concatinating your JS files, you generate a source map that holds information about your original files. This allows for querying lines in generated JS files, that then does a lookup in the source map and returns the original location. Modern dev tools can parse the source map automatically to make it appear as if you're running unminified/uncat files. 

## How does the source map work? 

Currently the only compiler/minifier that has support for source map generation is the Closure compiler. 

The special comment below is required at the end of the source map file and signifies to a browser's dev tools that a source map is available

`//# sourceMappingURL=/path/to/file.js.map`

Alternatively, you can add the following comment on your compiled JS file to do the same thing: 

`X-SourceMap: /path/to/file.js.map`

## How do I generate a source map?

Using the Closure comiler, the command is as follows:

```
java -jar compiler.jar \ 
     --js script.js \
     --create_source_map ./script-min.js.map \
     --source_map_format=V3 \
     --js_output_file script-min.js
```

## The anatomy of a source map

```
{
    version : 3,
    file: "out.js",
    sourceRoot : "",
    sources: ["foo.js", "bar.js"],
    names: ["src", "maps", "are", "fun"],
    mappings: "AAgBC,SAAQ,CAAEA"
}
```

Above, most of the info is self explanitory, but let's go over the last mappings property. Mappings uses Base64 VLQ values to save hella space (!!).

