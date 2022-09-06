<script>
  import JSZip, { file } from "jszip";
  import Img from "./lib/Img.svelte";
  import AsyncImg from "./lib/AsyncImg.svelte";
  let input;

  // https://svelte.dev/repl/b5333059a2f548809a3ac3f60a17a8a6?version=3.31.2
  let image;

  let src, alt, showImg;

  let fileList = [];

  let zipFile;
  let zipCompleted = false;

  let promise;

  function longest_common_starting_substring(arr1) {
    const arr = arr1.concat().sort();
    const a1 = arr[0];
    const a2 = arr[arr.length - 1];
    const L = a1.length;
    let i = 0;
    while (i < L && a1.charAt(i) === a2.charAt(i)) i++;
    return a1.substring(0, i);
  }

  function onChange() {
    const file = input.files[0];

    // https://stuk.github.io/jszip/documentation/examples/read-local-file-api.html
    JSZip.loadAsync(file).then(
      function (zip) {
        zipFile = zip;
        zipCompleted = true;

        zip.forEach(function (relativePath, zipEntry) {
          fileList.push({ name: zipEntry.name, pos: NaN, src: "" });
        });

        let fileNameCommonPart = longest_common_starting_substring(
          fileList.map(function (i) {
            return i.name;
          })
        );
        // console.log("Filename's common part is: " + fileNameCommonPart);

        fileList.forEach(function (item) {
          if (item.name.indexOf(fileNameCommonPart) != 0) {
            throw "CommonPart is not from the start for the file: " + item.name;
          }
          let fileNameLong = item.name;
          let ext = fileNameLong.split(".")[1];
          let fileName = fileNameLong.split("." + ext)[0];
          let fileNum = parseInt(fileName.split(fileNameCommonPart)[1]);
          item.pos = fileNum;
        });

        fileList.sort(function (a, b) {
          return a.pos - b.pos;
        });

        console.log(fileList[0].name);
        //https://stuk.github.io/jszip/documentation/api_zipobject/async.html

        // zip
        //   .file(fileList[0].name)
        //   .async("base64")
        //   .then(function (base64Str) {
        //     //https://jsfiddle.net/SXFwP/
        //     let data = "data:image/png;base64," + base64Str;
        //     // image.setAttribute("src", data);
        //     // image.setAttribute("alt", fileList[0].name);

        //     src = base64Str;
        //     alt = fileList[0].name;
        //     showImg = true;
        //   });

        // a component that uses promise results directly????

        for (let i = 0; i < fileList.length; i++) {
          zip
            .file(fileList[i].name)
            .async("base64")
            .then((url) => (fileList[i].src = url));
        }
      },
      function (e) {
        console.log(e);
        throw "Error reading " + file.name + ": " + e.message;
      }
    );
  }
</script>

<main>
  <div>
    <input type="file" bind:this={input} on:change={onChange} />
  </div>
  <div>
    <!-- <img bind:this={image} src="" alt="" /> -->
  </div>
  {#if fileList}
    {#each fileList as file}
      <Img src={file.src} alt={file.name} />
    {/each}
  {/if}
</main>
