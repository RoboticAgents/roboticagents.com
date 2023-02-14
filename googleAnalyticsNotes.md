# Code to setup Google Analyitics

## Date:

13 Feb 2023

## Site: 

Learn Robotic Agents 

## Use at Netlify. Place in __Build Snippet_ under the _Build & deploy_ setting

```
<!-- Global site tag (gtag.js) - Google Analytics -->
<script async src="https://www.googletagmanager.com/gtag/js?id=G-X3Y3KK3SLQ"></script>
<script>
  window.dataLayer = window.dataLayer || [];
  function gtag(){dataLayer.push(arguments);}
  gtag('js', new Date());

  gtag('config', 'G-X3Y3KK3SLQ');
</script>
```

# add to the `config.toml` file. 
`googleAnalytics : "G-X3Y3KK3SLQ"`

