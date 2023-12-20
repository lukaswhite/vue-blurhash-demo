<template>
  <div>
    <header>
      <p>This very simple demo uses the <a href="https://www.npmjs.com/package/blurhash">blurhash</a> library to create a placeholder image, then uses Vue to transition between that and the original image once it's been loaded.</p>
      <p>Here's the Vue component to calculate and display the placeholder itself:</p>
    </header>
    <pre>
 <code id="htmlViewer" style="color:rgb(68, 68, 68); font-weight:400;background-color:rgb(240, 240, 240);background:rgb(240, 240, 240);display:block;padding: .5em;"><span style="color:rgb(68, 68, 68); font-weight:400;">&lt;<span style="color:rgb(68, 68, 68); font-weight:700;">template</span>&gt;</span>
    <span style="color:rgb(68, 68, 68); font-weight:400;">&lt;<span style="color:rgb(68, 68, 68); font-weight:700;">canvas</span> <span style="color:rgb(68, 68, 68); font-weight:400;">ref</span>=<span style="color:rgb(136, 0, 0); font-weight:400;">&quot;canvas&quot;</span> <span style="color:rgb(68, 68, 68); font-weight:400;">:width</span>=<span style="color:rgb(136, 0, 0); font-weight:400;">&quot;width&quot;</span> <span style="color:rgb(68, 68, 68); font-weight:400;">:height</span>=<span style="color:rgb(136, 0, 0); font-weight:400;">&quot;height&quot;</span>&gt;</span><span style="color:rgb(68, 68, 68); font-weight:400;">&lt;/<span style="color:rgb(68, 68, 68); font-weight:700;">canvas</span>&gt;</span>
<span style="color:rgb(68, 68, 68); font-weight:400;">&lt;/<span style="color:rgb(68, 68, 68); font-weight:700;">template</span>&gt;</span>

<span style="color:rgb(68, 68, 68); font-weight:400;">&lt;<span style="color:rgb(68, 68, 68); font-weight:700;">script</span>&gt;</span><span style="color:rgb(68, 68, 68); font-weight:400;">
    <span style="color:rgb(68, 68, 68); font-weight:700;">import</span> { decode } <span style="color:rgb(68, 68, 68); font-weight:700;">from</span> <span style="color:rgb(136, 0, 0); font-weight:400;">&quot;blurhash&quot;</span>;

    <span style="color:rgb(68, 68, 68); font-weight:700;">export</span> <span style="color:rgb(68, 68, 68); font-weight:700;">default</span> {
        <span style="color:rgb(68, 68, 68); font-weight:400;">name</span>: <span style="color:rgb(136, 0, 0); font-weight:400;">&#x27;VueBlurHash&#x27;</span>,
        <span style="color:rgb(68, 68, 68); font-weight:400;">props</span>: {
            <span style="color:rgb(68, 68, 68); font-weight:400;">hash</span>: {
                <span style="color:rgb(68, 68, 68); font-weight:400;">type</span>: <span class="hljs-title class_">String</span>,
                <span style="color:rgb(68, 68, 68); font-weight:400;">required</span>: <span style="color:rgb(120, 169, 96); font-weight:400;">true</span>
            },
            <span style="color:rgb(68, 68, 68); font-weight:400;">width</span>: {
                <span style="color:rgb(68, 68, 68); font-weight:400;">type</span>: <span class="hljs-title class_">Number</span>,
                <span style="color:rgb(68, 68, 68); font-weight:400;">required</span>: <span style="color:rgb(120, 169, 96); font-weight:400;">true</span>
            },
            <span style="color:rgb(68, 68, 68); font-weight:400;">height</span>: {
                <span style="color:rgb(68, 68, 68); font-weight:400;">type</span>: <span class="hljs-title class_">Number</span>,
                <span style="color:rgb(68, 68, 68); font-weight:400;">required</span>: <span style="color:rgb(120, 169, 96); font-weight:400;">true</span>
            }
        },
        <span class="hljs-title function_">data</span>(<span style="color:rgb(68, 68, 68); font-weight:400;"></span>) {
            <span style="color:rgb(68, 68, 68); font-weight:700;">return</span> {
                <span style="color:rgb(68, 68, 68); font-weight:400;">rendered</span>: <span style="color:rgb(120, 169, 96); font-weight:400;">false</span>
            }
        },
        <span class="hljs-title function_">mounted</span>(<span style="color:rgb(68, 68, 68); font-weight:400;"></span>) {
            <span style="color:rgb(68, 68, 68); font-weight:700;">const</span> pixels = <span class="hljs-title function_">decode</span>(<span class="hljs-variable language_">this</span>.<span style="color:rgb(68, 68, 68); font-weight:400;">hash</span>, <span class="hljs-variable language_">this</span>.<span style="color:rgb(68, 68, 68); font-weight:400;">width</span>, <span class="hljs-variable language_">this</span>.<span style="color:rgb(68, 68, 68); font-weight:400;">height</span>)
            <span style="color:rgb(68, 68, 68); font-weight:700;">const</span> ctx = <span class="hljs-variable language_">this</span>.<span style="color:rgb(68, 68, 68); font-weight:400;">$refs</span>.<span style="color:rgb(68, 68, 68); font-weight:400;">canvas</span>.<span class="hljs-title function_">getContext</span>(<span style="color:rgb(136, 0, 0); font-weight:400;">&quot;2d&quot;</span>)
            <span style="color:rgb(68, 68, 68); font-weight:700;">const</span> imageData = ctx.<span class="hljs-title function_">createImageData</span>(<span class="hljs-variable language_">this</span>.<span style="color:rgb(68, 68, 68); font-weight:400;">width</span>, <span class="hljs-variable language_">this</span>.<span style="color:rgb(68, 68, 68); font-weight:400;">height</span>)
            imageData.<span style="color:rgb(68, 68, 68); font-weight:400;">data</span>.<span class="hljs-title function_">set</span>(pixels)
            ctx.<span class="hljs-title function_">putImageData</span>(imageData, <span style="color:rgb(136, 0, 0); font-weight:400;">0</span>, <span style="color:rgb(136, 0, 0); font-weight:400;">0</span>)
            <span class="hljs-variable language_">this</span>.<span style="color:rgb(68, 68, 68); font-weight:400;">rendered</span> = <span style="color:rgb(120, 169, 96); font-weight:400;">true</span>
            <span class="hljs-variable language_">this</span>.$emit(<span style="color:rgb(136, 0, 0); font-weight:400;">&#x27;rendered&#x27;</span>)
        }
    }
</span><span style="color:rgb(68, 68, 68); font-weight:400;">&lt;/<span style="color:rgb(68, 68, 68); font-weight:700;">script</span>&gt;</span>
</code></pre>
    <footer>Created by <a href="https://lukaswhite.com">Lukas White</a> | Photo by <a href="https://unsplash.com/@neom?utm_content=creditCopyText&utm_medium=referral&utm_source=unsplash">NEOM</a> on <a href="https://unsplash.com/photos/a-person-swimming-in-the-ocean-with-a-lot-of-fish-HXW26Gw8bk4?utm_content=creditCopyText&utm_medium=referral&utm_source=unsplash">Unsplash</a>
    </footer>
  </div>
</template>
