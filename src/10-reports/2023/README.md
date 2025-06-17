<script>
  function resizeIframe(obj) {
    obj.style.height = obj.contentWindow.document.documentElement.scrollHeight + 'px';
  }
</script>
<!-- <iframe src="./report-bck.html" title="Marvin HPC use report" style="min-width: 120%;height:100%;border:none;" frameborder="0"></iframe> -->
<iframe src="./report.html" title="Marvin HPC use report" frameborder="0" scrolling="no" width="120%" onload="resizeIframe(this);" />
 
