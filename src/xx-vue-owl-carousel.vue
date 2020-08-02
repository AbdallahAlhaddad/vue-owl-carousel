<template>
  <div>
    <div :id="elementHandle" class="owl-carousel owl-theme">
      <slot />
    </div>
  </div>
</template>
<script>
import "./jquery-global";
let $ = window.jQuery;
import "owl.carousel/dist/assets/owl.carousel.css";
import "owl.carousel/dist/assets/owl.theme.default.css";
import "owl.carousel";

export default {
  name: "VOwlCarousel",
  props: {
    slideValue: {
      type: Number,
      default: 0,
    },
    events: {
      type: Array,
      default: () => [],
    },
    rtl: {
      type: Boolean,
      default: false,
    },
    items: {
      type: Number,
      default: 3,
    },
    margin: {
      type: Number,
      default: 0,
    },
    loop: {
      type: Boolean,
      default: false,
    },
    center: {
      type: Boolean,
      default: false,
    },
    mouseDrag: {
      type: Boolean,
      default: true,
    },
    touchDrag: {
      type: Boolean,
      default: true,
    },
    pullDrag: {
      type: Boolean,
      default: true,
    },
    freeDrag: {
      type: Boolean,
      default: false,
    },
    stagePadding: {
      type: Number,
      default: 0,
    },
    merge: {
      type: Boolean,
      default: false,
    },
    mergeFit: {
      type: Boolean,
      default: false,
    },
    autoWidth: {
      type: Boolean,
      default: false,
    },
    startPosition: {
      type: Number,
      default: 0,
    },
    uRLhashListener: {
      type: Boolean,
      default: false,
    },
    nav: {
      type: Boolean,
      default: true,
    },
    rewind: {
      type: Boolean,
      default: true,
    },
    navText: {
      type: Array,
      default: () => ["prev", "next"],
    },
    navElement: {
      type: String,
      default: "div",
    },
    slideBy: {
      type: [Number, String],
      default: 1,
    },
    slideTransition: {
      type: String,
      default: "",
    },
    dots: {
      type: Boolean,
      default: true,
    },
    dotsEach: {
      type: [Number, Boolean],
      default: false,
    },
    dotsData: {
      type: Boolean,
      default: false,
    },
    lazyLoad: {
      type: Boolean,
      default: false,
    },
    lazyLoadEager: {
      type: Number,
      default: 0,
    },
    autoplay: {
      type: Boolean,
      default: false,
    },
    autoplaySpeed: {
      type: Boolean,
      default: false,
    },
    autoplayTimeout: {
      type: Number,
      default: 5000,
    },
    autoplayHoverPause: {
      type: Boolean,
      default: false,
    },
    smartSpeed: {
      type: Number,
      default: 250,
    },
    fluidSpeed: {
      type: [Number, Boolean],
      default: false,
    },
    navSpeed: {
      type: [Number, Boolean],
      default: false,
    },
    dragEndSpeed: {
      type: [Number, Boolean],
      default: false,
    },
    callbacks: {
      type: Boolean,
      default: true,
    },
    responsive: {
      type: Object,
      default: () => ({}),
    },
    responsiveRefreshRate: {
      type: Number,
      default: 200,
    },
    responsiveBaseElement: {
      type: String,
      default: "window",
    },
    video: {
      type: Boolean,
      default: false,
    },
    videoHeight: {
      type: [Number, Boolean],
      default: false,
    },
    videoWidth: {
      type: [Number, Boolean],
      default: false,
    },
    animateOut: {
      type: [String, Boolean],
      default: false,
    },
    animateIn: {
      type: [String, Boolean],
      default: false,
    },
    fallbackEasing: {
      type: String,
      default: "swing",
    },
    info: {
      type: Function,
      default: () => {},
    },
    itemElement: {
      type: String,
      default: "div",
    },
    stageElement: {
      type: String,
      default: "div",
    },
    navContainer: {
      type: [String, Boolean],
      default: false,
    },
    dotsContainer: {
      type: [String, Boolean],
      default: false,
    },
    checkVisible: {
      type: Boolean,
      default: true,
    },
  },

  watch: {
    rtl(newValue, oldValue) {
      this.owl.trigger("destroy.owl.carousel");
      this.instantiate();
    },
    items(newValue, oldValue) {
      this.owl.trigger("destroy.owl.carousel");
      this.instantiate();
    },
    slideValue(newValue, oldValue) {
      if (newValue < oldValue) this.goPrev();
      else this.goNext();
    },
  },

  data() {
    return {
      owl: null,
      showPrev: false,
      showNext: true,
      cachedCurrentPos: null,
      elementHandle: "carousel_" + this.generateUniqueId(),
    };
  },

  mounted: function () {
    this.instantiate();
    this.bindEvents();
    this.handleCachedIndex();
  },

  methods: {
    instantiate() {
      /**
       *!  Notice that initialize.owl.carousel and initialized.owl.carousel
       *!  events must be attached before Owl Carousel initialization. This is required only for those two.
       **/
      $("#" + this.elementHandle).on("initialize.owl.carousel", (event) => {
        this.$emit("initialize", event);
      });
      $("#" + this.elementHandle).on("initialized.owl.carousel", (event) => {
        this.$emit("initialized", event);
      });

      this.owl = $("#" + this.elementHandle).owlCarousel({
        // ! see if there are a cached postion.. if not use the passed prop:
        startPosition: this.cachedCurrentPos
          ? this.cachedCurrentPos
          : this.startPosition,
        items: this.items,
        margin: this.margin,
        loop: this.loop,
        center: this.center,
        mouseDrag: this.mouseDrag,
        touchDrag: this.touchDrag,
        pullDrag: this.pullDrag,
        freeDrag: this.freeDrag,
        stagePadding: this.stagePadding,
        merge: this.merge,
        mergeFit: this.mergeFit,
        autoWidth: this.autoWidth,
        uRLhashListener: this.uRLhashListener,
        nav: this.nav,
        rewind: this.rewind,
        navText: this.navText,
        navElement: this.navElement,
        slideBy: this.slideBy,
        slideTransition: this.slideTransition,
        dots: this.dots,
        dotsEach: this.dotsEach,
        dotsData: this.dotsData,
        lazyLoad: this.lazyLoad,
        lazyLoadEager: this.lazyLoadEager,
        autoplay: this.autoplay,
        autoplaySpeed: this.autoplaySpeed,
        autoplayTimeout: this.autoplayTimeout,
        autoplayHoverPause: this.autoplayHoverPause,
        smartSpeed: this.smartSpeed,
        fluidSpeed: this.fluidSpeed,
        navSpeed: this.navSpeed,
        dragEndSpeed: this.dragEndSpeed,
        callbacks: this.callbacks,
        responsive: this.responsive,
        responsiveRefreshRate: this.responsiveRefreshRate,
        responsiveBaseElement: this.responsiveBaseElement,
        rtl: this.rtl,
        video: this.video,
        videoHeight: this.videoHeight,
        videoWidth: this.videoWidth,
        animateOut: this.animateOut,
        animateIn: this.animateIn,
        fallbackEasing: this.fallbackEasing,
        info: this.info,
        itemElement: this.itemElement,
        stageElement: this.stageElement,
        navContainer: this.navContainer,
        dotsContainer: this.dotsContainer,
        checkVisible: this.checkVisible,
      });

      // remove 'initialize','initialized' event listeners
      $("#" + this.elementHandle).off("initialize.owl.carousel");
      $("#" + this.elementHandle).off("initialized.owl.carousel");
    },
    generateUniqueId() {
      return Math.random().toString(36).substring(2, 15);
    },
    bindEvents() {
      this.events.forEach((eventName) => {
        this.owl.on(`${eventName}.owl.carousel`, (event) => {
          this.$emit(eventName, event);
          // console.log(eventName)
        });
      });
    },
    handleCachedIndex() {
      this.owl.on("changed.owl.carousel", (event) => {
        this.cachedCurrentPos = event.item.index;
      });
    },
    goNext() {
      this.owl.trigger("next.owl.carousel");
    },
    goPrev() {
      this.owl.trigger("prev.owl.carousel");
    },
  },
};
</script>
