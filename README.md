<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Bear Pop Game</title>
<style>
body {
  margin: 0;
  background: #48c1bb;
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
  user-select: none;
}
#bear {
  width: 100px;
  transition: transform 0.3s ease;
}
#donut {
  position: absolute;
  bottom: 50px;
  width: 50px;
  cursor: grab;
}
</style>
</head>
<body>
<img id="bear" src="https://upload.wikimedia.org/wikipedia/commons/thumb/1/1a/Bear_cartoon.svg/512px-Bear_cartoon.svg.png">
<img id="donut" src="https://upload.wikimedia.org/wikipedia/commons/thumb/9/9f/Donut.svg/512px-Donut.svg.png">
<script>
let bear = document.getElementById('bear')
let donut = document.getElementById('donut')
let feedCount = 0
donut.addEventListener('mousedown', e => {
  const move = e => {
    donut.style.left = e.pageX - 25 + 'px'
    donut.style.top = e.pageY - 25 + 'px'
  }
  const up = e => {
    document.removeEventListener('mousemove', move)
    document.removeEventListener('mouseup', up)
    let bearRect = bear.getBoundingClientRect()
    let donutRect = donut.getBoundingClientRect()
    if (
      donutRect.left < bearRect.right &&
      donutRect.right > bearRect.left &&
      donutRect.top < bearRect.bottom &&
      donutRect.bottom > bearRect.top
    ) {
      feedCount++
      bear.style.transform = `scale(${1 + feedCount * 0.05})`
      if (feedCount >= 10) {
        bear.style.transition = 'transform 0.2s ease'
        bear.style.transform = 'scale(0)'
        setTimeout(() => {
          feedCount = 0
          bear.style.transition = 'none'
          bear.style.transform = 'scale(0.2)'
          setTimeout(() => {
            bear.style.transition = 'transform 0.5s ease'
            bear.style.transform = 'scale(1)'
          }, 50)
        }, 200)
      }
    }
    donut.style.left = ''
    donut.style.top = ''
  }
  document.addEventListener('mousemove', move)
  document.addEventListener('mouseup', up)
})
</script>
</body>
</html>
```
