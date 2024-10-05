# Personal Webpage

This is my personal webpage, written using [Obsidian](https://obsidian.md/),
built using [Quartz 4](https://quartz.jzhao.xyz/).

## Build

### Development

To build for development:

```sh
npx quartz build --serve
```

> [!NOTE]
> This will host a local webpage at: `http://localhost:8080/`

**Additional Options:**

More details can be found [here](https://quartz.jzhao.xyz/build).

1. `-d` or `--directory`: the content folder. This is normally just content
1. `-v` or `--verbose`: print out extra logging information
1. `-o` or `--output`: the output folder. This is normally just public
1. `--serve`: run a local hot-reloading server to preview your Quartz
1. `--port`: what port to run the local preview server on
1. `--concurrency`: how many threads to use to parse notes
