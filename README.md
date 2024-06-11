## Hi there 👋

<picture>
  <source media="(prefers-color-scheme: dark)" srcset="https://raw.githubusercontent.com/novohool/novohool/output/github-contribution-grid-snake-dark.svg">
  <source media="(prefers-color-scheme: light)" srcset="https://raw.githubusercontent.com/novohool/novohool/output/github-contribution-grid-snake.svg">
  <img alt="github contribution grid snake animation" src="https://raw.githubusercontent.com/novohool/novohool/output/github-contribution-grid-snake.svg">
</picture>

_generated with [novohool/novohool](https://github.com/novohool/novohool)_

<code>
<iframe id="github-iframe" src=""></iframe>
<script>
    fetch('https://api.github.com/repos/ileathan/hubot-mubot/contents/src/mubot.coffee')
        .then(function(response) {
            return response.json();
        }).then(function(data) {
            var iframe = document.getElementById('github-iframe');
            iframe.src = 'data:text/html;base64,' + encodeURIComponent(data['content']);
        });
</script>
</code>
