<script lang="ts">
  import { onMount } from "svelte";

  export let method = "letters";
  let container;

  let elems;
  let str = "eefec303079ad17405c889e092e105b0";

  let replaceBreaks = function (elem: any) {
    var r = document.createTextNode(str);
    Array.prototype.slice
      .call(elem.querySelectorAll("br"))
      .forEach(function (br) {
        elem.replaceChild(r.cloneNode(), br);
      });
  };
  let wrap = function (
    elems: [],
    splitStr: String,
    className: String,
    after: String,
    breaks: Boolean
  ) {
    for (let elem of elems.childNodes) {
      let elemtomodify;
      if (elem.nodeName === "#text") {
        let wrap = document.createElement("div");
        wrap.innerHTML = elem.nodeValue.trim();
        elem.replaceWith(wrap);
        elemtomodify = wrap;
      } else {
        elemtomodify = elem;
      }
      console.log(elemtomodify.textContent);
      var original = elemtomodify.textContent;
      if (breaks) {
        replaceBreaks(elemtomodify);
      }
      var text = elemtomodify.textContent
        .split(splitStr)
        .map(function (item, index) {
          return (
            '<span class="' +
            className +
            " " +
            className +
            (index + 1) +
            '" aria-hidden="true">' +
            item +
            "</span>" +
            after
          );
        })
        .join("");
      elemtomodify.setAttribute("aria-label", original);
      elemtomodify.innerHTML = text;
    }
    return elems;
  };

  onMount(() => {
    // elems = container.children;
    if (["letters", "words", "lines"].indexOf(method) === -1)
      return console.error(
        "please provide correct Sveltering method. \n ['letters', 'words', 'lines']"
      );
    if (method === "letters") wrap(container, "", "char", "");
    if (method === "words") wrap(container, " ", "word", " ");
    if (method === "lines") wrap(container, str, "line", "", true);
  });
</script>

<div bind:this={container}>
  <slot />
</div>
