# markdown

````javascript
import 'materialize-css/dist/css/materialize.css';
import 'prismjs/themes/prism.css';
import './style.css';
import $ from 'jquery';
import 'materialize-css/dist/js/materialize';
import Prism from 'prismjs';

M.AutoInit();

let MarkdownIt = require('markdown-it');

let md = new MarkdownIt({
  highlight(str, lang) {
    let hl;
    try {
      hl = Prism.highlight(str, Prism.languages[lang])
    } catch (error) {
      hl = md.utils.escapeHtml(str)
    }
    return `<pre class="language-${lang}"><code class="language-${lang}">${hl}</code></pre>`
  }
});

$('.link').click(function (e) {
  e.preventDefault();
  let page = $(this).attr('href');
  $.ajax({
    url: page,
    dataType: "text",
    success: function (data) {
      $("#content").html(md.render(data));
    }
  });
  return false;
});

````
