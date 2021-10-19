<template>
  <header id="header" class="fixed-top d-flex align-items-center header-transparent">
    <div class="container d-flex justify-content-between align-items-center">
      <div id="logo">
        <a href="index.html">Random Photo Sharing App</a>
      </div>
      <nav id="navbar" class="navbar">
        <ul>
          <li class="dropdown">
            <a href=""><span>About Me</span></a>
            <ul>
              <li><a href="https://yasindemirkaya.com/" target="_blank">Website</a></li>
              <li class="dropdown">
                <a href=""><span>Social</span></a>
                <ul>
                  <li>
                    <a href="https://github.com/yasindemirkaya" target="_blank">GitHub Repository</a>
                  </li>
                </ul>
              </li>
            </ul>
          </li>
        </ul>
      </nav>
    </div>
  </header>
</template>

<script>
export default {
  name: "Header",
};
</script>

<style></style>
