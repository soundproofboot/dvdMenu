<script>
  let divWidth=0;
    let divHeight=0;
    
    let windowHeight=0,
    windowWidth=0;

    $: topOffset = Math.random() * (windowHeight - divHeight);
    $: leftOffset = Math.random() * (windowWidth - divWidth);

    $: boxStyle = `top: ${topOffset}px; left: ${leftOffset}px; ${getLogoSize()}`;

    let down = Math.random() > .5 ? true : false;
    let right = Math.random() < .5 ? true : false;

    function getLogoSize () {
        if (windowHeight < windowWidth) return `height: ${windowHeight * .25}px`;
        return `width: ${windowWidth * .25}px`;
    }

    setInterval(() => {
        if (down) {
            if (topOffset < windowHeight-divHeight) topOffset++;
            else if (topOffset >= windowHeight-divHeight) down = false;
        }
        if (!down) {
            if (topOffset > 0) topOffset--;
            else if (topOffset <= 0) down = true; 
        }
        if (right) {
            if (leftOffset < windowWidth - divWidth) leftOffset++;
            else if (leftOffset >= windowWidth - divWidth) right = false;
        }
        if (!right) {
            if (leftOffset > 0) leftOffset--;
            else if (leftOffset <= 0) right = true;
        }
    }, 20)
</script>
  <svelte:head><link rel="icon" type="image/svg+xml" href="DVD_icon.svg" sizes="any"/></svelte:head>
  <svelte:window bind:innerHeight={windowHeight} bind:innerWidth={windowWidth} on:resize={() => {
    topOffset = 0;
    leftOffset = 0
  }}/>
  <div bind:clientHeight={divHeight} bind:clientWidth={divWidth}  style={boxStyle}>
    <img src='DVD_icon.svg' alt="DVD Logo" />
  </div>

<style>
    div {
        animation: rainbow 60s linear infinite;
        position: absolute;
    }

    img {
        height: 100%;
    }

    @keyframes rainbow {
        from {
            background-color: red;
        }

        14% {
            background-color: orange;
        }

        28% {
            background-color: yellow;
        }

        42% {
            background-color: green;
        }

        56% {
            background-color: blue;
        }

        70% {
            background-color: indigo;
        }

        84% {
            background-color: violet;
        }

        to {
            background-color: red;
        }
    }
</style>
