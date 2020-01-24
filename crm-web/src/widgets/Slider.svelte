<style>
  .mdc-slider {
    position: relative;
    width: 100%;
    height: 48px;
    cursor: pointer;
    -ms-touch-action: pan-x;
    touch-action: pan-x;
    -webkit-tap-highlight-color: rgba(0, 0, 0, 0);
  }

  .mdc-slider:not(.mdc-slider--disabled) .mdc-slider__track-container {
    background-color: rgba(1, 135, 134, .26);
  }

  .mdc-slider__track-container {
    position: absolute;
    top: 50%;
    width: 100%;
    height: 2px;
    overflow: hidden;
  }

  .mdc-slider:not(.mdc-slider--disabled) .mdc-slider__track {
    background-color: #018786;
  }

  .mdc-slider__track {
    position: absolute;
    width: 100%;
    height: 100%;
    -webkit-transform-origin: left top;
    -ms-transform-origin: left top;
    transform-origin: left top;
    will-change: transform;
  }

  .mdc-slider__thumb-container {
    position: absolute;
    top: 15px;
    left: 0;
    width: 21px;
    height: 100%;
    -webkit-user-select: none;
    -moz-user-select: none;
    -ms-user-select: none;
    user-select: none;
    will-change: transform;
  }

  .mdc-slider__thumb {
    position: absolute;
    top: 0;
    left: 0;
    -webkit-transform: scale(.571);
    -ms-transform: scale(.571);
    transform: scale(.571);
    stroke-width: 3.5;
    -webkit-transition: fill .1s ease-out, stroke .1s ease-out, -webkit-transform .1s ease-out;
    transition: fill .1s ease-out, stroke .1s ease-out, -webkit-transform .1s ease-out;
    -o-transition: transform .1s ease-out, fill .1s ease-out, stroke .1s ease-out;
    transition: transform .1s ease-out, fill .1s ease-out, stroke .1s ease-out;
    transition: transform .1s ease-out, fill .1s ease-out, stroke .1s ease-out, -webkit-transform .1s ease-out;
  }

  .mdc-slider__focus-ring {
    width: 21px;
    height: 21px;
    border-radius: 50%;
    opacity: 0;
    -webkit-transition: opacity .26667s ease-out, background-color .26667s ease-out, -webkit-transform .26667s ease-out;
    transition: opacity .26667s ease-out, background-color .26667s ease-out, -webkit-transform .26667s ease-out;
    -o-transition: transform .26667s ease-out, opacity .26667s ease-out, background-color .26667s ease-out;
    transition: transform .26667s ease-out, opacity .26667s ease-out, background-color .26667s ease-out;
    transition: transform .26667s ease-out, opacity .26667s ease-out, background-color .26667s ease-out, -webkit-transform .26667s ease-out;
  }
</style>

<div class="mdc-slider" tabindex="0" role="slider" aria-valuemin="0" aria-valuemax="100"
     aria-valuenow="45.135467980295566" aria-label="Select Value">
  <div class="mdc-slider__track-container">
    <div class="mdc-slider__track" style="transform: scaleX(0.451355);"></div>
  </div>
  <div class="mdc-slider__thumb-container"
       style="transform: translateX(366.5px) translateX(-50%);">
    <svg class="mdc-slider__thumb" width="21" height="21">
      <circle cx="10.5" cy="10.5" r="7.875"></circle>
    </svg>
    <div class="mdc-slider__focus-ring"></div>
  </div>
</div>
