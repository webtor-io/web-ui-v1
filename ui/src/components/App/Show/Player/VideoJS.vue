<template>
</template>

<script>
import videojs from 'video.js';
window.videojs = videojs;
require('videojs-contrib-hls/dist/videojs-contrib-hls');
import {mapState} from 'vuex';
export default {
  computed: {
    ...mapState({
      source: (state) => state.source,
    })
  },
  watch: {
    source() {
      this.$forceUpdate();
    },
  },
  updated() {
    const {src, type} = this.$store.state.source;
    if (this.$video) videojs(this.$video).dispose();
    this.$video = document.createElement('video');
    this.$video.className = 'video-js vjs-sublime-skin';
    this.$el.appendChild(this.$video);
    const player = videojs(this.$video, {
      controls: true,
      autoplay: true,
      preload: 'auto',
      width: 640,
    });
    player.src([{src, type}]);
  }
};
</script>

<style src='video.js/dist/video-js.css'></style>
<style>
/* https://codepen.io/zanechua/pen/GozrNe */
.video-js {
  /* The base font size controls the size of everything, not just text.
     All dimensions use em-based sizes so that the scale along with the font size.
     Try increasing it to 15px and see what happens. */
  font-size: 10px;
  /* The main font color changes the ICON COLORS as well as the text */
  color: #fff;
}

/* The "Big Play Button" is the play button that shows before the video plays.
   To center it set the align values to center and middle. The typical location
   of the button is the center, but there is trend towards moving it to a corner
   where it gets out of the way of valuable content in the poster image.*/
.vjs-sublime-skin .vjs-big-play-button {
  /* The font size is what makes the big play button...big.
     All width/height values use ems, which are a multiple of the font size.
     If the .video-js font-size is 10px, then 3em equals 30px.*/
  font-size: 8em;
  /* We're using SCSS vars here because the values are used in multiple places.
     Now that font size is set, the following em values will be a multiple of the
     new font size. If the font-size is 3em (30px), then setting any of
     the following values to 3em would equal 30px. 3 * font-size. */
  /* 1.5em = 45px default */
  line-height: 1.5em;
  height: 1.5em;
  width: 3em;
  /* 0.06666em = 2px default */
  border: 0;
  /* 0.3em = 9px default */
  border-radius: 0.3em;
  /* Align center */
  left: 50%;
  top: 50%;
  margin-left: -1.5em;
  margin-top: -0.75em;
}

/* The default color of control backgrounds is mostly black but with a little
   bit of blue so it can still be seen on all-black video frames, which are common. */
.video-js .vjs-control-bar,
.video-js .vjs-big-play-button,
.video-js .vjs-menu-button .vjs-menu-content {
  /* IE8 - has no alpha support */
  background-color: #2B333F;
  /* Opacity: 1.0 = 100%, 0.0 = 0% */
  background-color: rgba(43, 51, 63, 0.7);
  background-color: transparent;
}

/* Slider - used for Volume bar and Progress bar */
.video-js .vjs-slider {
  background-color: #73859f;
  background-color: rgba(115, 133, 159, 0.5);
  background-color: rgba(255, 255, 255, 0.3);
  border-radius: 2px;
  height: 6.5px;
}

/* The slider bar color is used for the progress bar and the volume bar
   (the first two can be removed after a fix that's coming) */
.video-js .vjs-volume-level,
.video-js .vjs-play-progress,
.video-js .vjs-slider-bar {
  background: #fff;
}

/* Enlarged Slider to enable easier tracking. Adjust all the height:6.5px to preferred height for the slider if necessary. */
.video-js .vjs-progress-holder .vjs-load-progress,
.video-js .vjs-progress-holder .vjs-load-progress div,
.video-js .vjs-progress-holder .vjs-play-progress,
.video-js .vjs-progress-holder .vjs-tooltip-progress-bar {
  height: 6.5px;
}

/* The main progress bar also has a bar that shows how much has been loaded. */
.video-js .vjs-load-progress {
  /* For IE8 we'll lighten the color */
  background: ligthen(#73859f, 25%);
  /* Otherwise we'll rely on stacked opacities */
  background: rgba(115, 133, 159, 0.5);
}

/* The load progress bar also has internal divs that represent
   smaller disconnected loaded time ranges */
.video-js .vjs-load-progress div {
  /* For IE8 we'll lighten the color */
  background: ligthen(#73859f, 50%);
  /* Otherwise we'll rely on stacked opacities */
  background: rgba(115, 133, 159, 0.75);
}

.vjs-sublime-skin .vjs-poster {
  outline: none;
  /* Remove Blue Outline on Click*/
  outline: 0;
}

.vjs-sublime-skin:hover .vjs-big-play-button {
  background-color: transparent;
}

.vjs-sublime-skin .vjs-fullscreen-control:before,
.vjs-sublime-skin.vjs-fullscreen .vjs-fullscreen-control:before {
  content: '';
  /* Remove Fullscreen Exit Icon */
}

.vjs-sublime-skin.vjs-fullscreen .vjs-fullscreen-control {
  background: #fff;
}

.vjs-sublime-skin .vjs-fullscreen-control {
  border: 3px solid #fff;
  box-sizing: border-box;
  cursor: pointer;
  margin-top: -7px;
  top: 50%;
  height: 14px;
  width: 22px;
  margin-right: 10px;
}

.vjs-sublime-skin.vjs-fullscreen .vjs-fullscreen-control:after {
  background: #000;
  content: "";
  display: block;
  position: absolute;
  bottom: 0;
  left: 0;
  height: 5px;
  width: 5px;
}

.vjs-sublime-skin .vjs-progress-holder {
  margin: 0;
}

.vjs-sublime-skin .vjs-progress-control .vjs-progress-holder:after {
  border-radius: 2px;
  display: block;
  height: 6.5px;
}

.vjs-sublime-skin .vjs-progress-control .vjs-load-progres,
.vjs-sublime-skin .vjs-progress-control .vjs-play-progress {
  border-radius: 2px;
  height: 6.5px;
}

.vjs-sublime-skin .vjs-playback-rate {
  display: none;
  /* Remove Playback Rate */
}

.vjs-sublime-skin .vjs-progress-control {
  margin-right: 50px;
}

.vjs-sublime-skin .vjs-time-control {
  right: 55px;
}

.vjs-sublime-skin .vjs-volume-menu-button:before {
  width: 1.2em;
  z-index: 1;
}

.vjs-sublime-skin .vjs-volume-menu-button .vjs-menu,
.vjs-sublime-skin .vjs-volume-menu-button:focus .vjs-menu,
.vjs-sublime-skin .vjs-volume-menu-button.vjs-slider-active .vjs-menu {
  display: block;
  opacity: 1;
}

.vjs-sublime-skin .vjs-volume-menu-button, .vjs-sublime-skin .vjs-volume-panel {
  width: 6em;
  position: absolute;
  right: 0;
  margin-right: 30px;
}

.vjs-sublime-skin .vjs-volume-menu-button .vjs-menu-content,
.vjs-sublime-skin .vjs-volume-menu-button:hover,
.vjs-sublime-skin .vjs-volume-menu-button:focus,
.vjs-sublime-skin .vjs-volume-menu-button.vjs-slider-active,
.vjs-sublime-skin .vjs-volume-panel .vjs-volume-control,
.vjs-sublime-skin .vjs-volume-panel:hover,
.vjs-sublime-skin .vjs-volume-panel:focus,
.vjs-sublime-skin .vjs-volume-panel.vjs-slider-active {
  width: 6em;
}

.vjs-sublime-skin .vjs-volume-menu-button .vjs-menu {
  left: 23px;
}

.vjs-sublime-skin .vjs-mouse-display:before,
.vjs-sublime-skin .vjs-play-progress:before,
.vjs-sublime-skin .vjs-volume-level:before {
  content: '';
  /* Remove Circle From Progress Bar */
}

.vjs-sublime-skin .vjs-mouse-display:after,
.vjs-sublime-skin .vjs-play-progress:after,
.vjs-sublime-skin .vjs-time-tooltip {
  width: 5.5em;
}

.vjs-sublime-skin .vjs-audio-button {
  display: none;
}

.vjs-sublime-skin .vjs-volume-bar {
  background: url(data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAACwAAAAcCAQAAACw95UnAAAAMElEQVRIx2NgoBL4n4YKGUYNHkEG4zJg1OCRYDCpBowaPJwMppbLRg0eNXjUYBLEAXWNUA6QNm1lAAAAAElFTkSuQmCC);
  background-size: 22px 14px;
  background-repeat: no-repeat;
  height: 100%;
  width: 100%;
  max-width: 22px;
  max-height: 14px;
  margin: 7px 4px;
  border-radius: 0;
}

.vjs-sublime-skin .vjs-volume-level {
  background: url(data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAACwAAAAcAQAAAAAyhWABAAAAAnRSTlMAAHaTzTgAAAAZSURBVHgBYwAB/g9EUv+JokCqiaT+U4MCAPKPS7WUUOc1AAAAAElFTkSuQmCC);
  background-size: 22px 14px;
  background-repeat: no-repeat;
  max-width: 22px;
  max-height: 14px;
  height: 100%;
}

/* New for VideoJS v6 */
.vjs-sublime-skin .vjs-volume-panel.vjs-volume-panel-horizontal.vjs-slider-active,
.vjs-sublime-skin .vjs-volume-panel.vjs-volume-panel-horizontal:active,
.vjs-sublime-skin .vjs-volume-panel.vjs-volume-panel-horizontal:focus,
.vjs-sublime-skin .vjs-volume-panel.vjs-volume-panel-horizontal:hover {
  width: 6em;
  transition-property: none;
}

.vjs-sublime-skin .vjs-volume-panel .vjs-mute-control:hover
~ .vjs-volume-control.vjs-volume-horizontal {
  width: 3em;
  height: auto;
}

.vjs-sublime-skin .vjs-volume-panel .vjs-mute-control:hover
~ .vjs-volume-control {
  transition-property: none;
}

.vjs-sublime-skin .vjs-fullscreen-control .vjs-icon-placeholder {
  display: none;
  /* Remove Duplicate Fullscreen Icon */
}

.vjs-sublime-skin .vjs-volume-panel .vjs-mute-control {
  width: 2em;
  z-index: 1;
  padding: 0;
}

.vjs-sublime-skin .vjs-volume-panel .vjs-volume-control {
  display: inline-block;
  position: relative;
  left: 5px;
  opacity: 1;
  width: 3em;
  height: auto;
}

</style>
