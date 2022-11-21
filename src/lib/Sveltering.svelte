<script>
  import { onMount } from "svelte";

  export let method = "letters";
  let container;
  let elems;
  let str = "eefec303079ad17405c889e092e105b0";

  let replaceBreaks = function (elem) {
    var r = document.createTextNode(str);
    Array.prototype.slice
      .call(elem.querySelectorAll("br"))
      .forEach(function (br) {
        elem.replaceChild(r.cloneNode(), br);
      });
  };
  let wrap = function (elems, splitStr, className, after, breaks) {
    for (let elem of elems) {
      var original = elem.textContent;
      if (breaks) {
        replaceBreaks(elem);
      }
      var text = elem.textContent
        .split(splitStr)
        .map(function (item, index) {
          return (
            '<span class="' +
            className +
            (index + 1) +
            '" aria-hidden="true">' +
            item +
            "</span>" +
            after
          );
        })
        .join("");
      elem.setAttribute("aria-label", original);
      elem.innerHTML = text;
    }
    return elems;
  };

  onMount(() => {
    elems = container.children;
    console.log(["letters", "words", "lines"].indexOf(method));
    // if (method !== "letters") return console.error("please provide method");
    if (["letters", "words", "lines"].indexOf(method) === -1)
      return console.error(
        "please provide correct Sveltering method. \n ['letters', 'words', 'lines']"
      );
    if (method === "letters") wrap(elems, "", "char", "");
    if (method === "words") wrap(elems, " ", "word", " ");
    if (method === "lines") wrap(elems, str, "line", "", true);
    for (let elem of elems) {
      container.appendChild(elem);
    }
  });
</script>

<div bind:this={container}>
  <slot />
</div>
