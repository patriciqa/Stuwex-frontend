<template>
  <body>
    <div class="welcome-page" id="welcome-page">
      <div class="welcome-content">
        <section id="kreis">
          <svg class="circle progress-circle" width="260" height="260">
            <path
              d="M130,16.8c62.5,0,113.2,50.6,113.2,113.2S192.5,243.2,130,243.2S16.8,192.5,16.8,130S67.5,16.8,130,16.8z"
            />
          </svg>
          <svg class="circle progress-circle-dashed" width="260" height="260">
            <path
              d="M130,16.8c62.5,0,113.2,50.6,113.2,113.2S192.5,243.2,130,243.2S16.8,192.5,16.8,130S67.5,16.8,130,16.8z"
            />
          </svg>
          <svg
            class="building"
            width="347"
            height="215"
            viewBox="0 0 347 215"
            fill="none"
            xmlns="http://www.w3.org/2000/svg"
          >
            <path
              d="M37.1353 210L4 207.287V76.2159L37.1353 61.9727M37.1353 210L322.609 207.287M37.1353 210V143.701M37.1353 61.9727L234.078 82.4897M37.1353 61.9727V117.223M322.609 207.287H343V13.9868L315.472 5M322.609 207.287V146.754M234.078 82.4897V40.7775L315.472 5M234.078 82.4897L315.472 91.6195M315.472 5V91.6195M315.472 91.6195L322.609 92.1547V110.637M37.1353 117.223L322.609 127.593M37.1353 117.223V143.701M322.609 127.593V146.754M322.609 127.593V119.793V110.637M37.1353 91.1373L322.609 110.637M37.1353 143.701L322.609 146.754"
            />
          </svg>
        </section>
        <section id="welcome-text">
          <p class="welcome-text welcome-text-heading">
            Grosssiedlungen in Pressebildern
          </p>
          <p class="welcome-text welcome-text-subheading">
            Hoffnungsträger oder Symbol der Wachstumskritik?
          </p>
        </section>
      </div>
    </div>
  </body>
</template>



<script>
export default {
  mounted() {
    gsap.registerPlugin(ScrollTrigger);

    var path = document.getElementsByTagName("path");
    var pathLength = path[0].getTotalLength();
    console.log(pathLength);

    var currentPathLength = pathLength;
    var step = 2;
    var percent = 0;
    function changeToHome() {
      if (percent > 0.95) {
        console.log("yuhu");
      }
    }
    function doAnim() {
      path[0].style.strokeDashoffset = pathLength * (1 - percent);
    }

    gsap.to("#kreis", {
      scrollTrigger: {
        trigger: "#welcome-page",
        onUpdate: (self) => {
          // console.log(self.progress)
          percent = self.progress;
          console.log(percent);
          changeToHome();
          doAnim();
        },
        // markers: true,
        start: "top 0.1%",
        end: "bottom 100%",
      },
    });
  },
};
</script>



<style scoped>
body {
  background-color: var(--black);
  color: var(--white);
}

.welcome-text {
  text-align: center;
}

.welcome-text-heading {
  font-family: "IBM Plex Sans";
  font-weight: 600;
  font-size: 4rem;
}

.welcome-text-subheading {
  font-size: 1.5rem;
}

.welcome-page {
  display: flex;
  flex-direction: column;
  height: 150vh;
  align-items: center;
  justify-content: center;
}

.welcome-content {
  position: fixed;
  height: 100%;
  padding-top: 5vh;
}

.circle {
  transform: scale(2.5);
}

.building {
  stroke-width: 1;
}

.building path {
  stroke-width: 3;
  stroke: var(--red);
}

#kreis {
  display: grid;
  grid-template-rows: 1fr;
  grid-template-columns: 1fr;
  grid-template-areas:
    "centerfix"
    "centerfix";
  justify-content: center;
  margin-bottom: 10vh;
}
#kreis svg {
  grid-area: centerfix;
  margin: 0 auto;
}

.circle path {
  stroke: #fff;
  fill: none;
  margin: 0 auto;
  justify-content: center;
  position: sticky;
}

.progress-circle path {
  stroke-dasharray: 711;
  stroke-dashoffset: 0;
  stroke-width: 1;
}

.progress-circle-dashed {
  stroke-dasharray: 4 6;
  stroke-width: 1;
  z-index: -1;
}

/* Scrollbar fix */
template {
  -ms-overflow-style: none; /* for Internet Explorer, Edge */
  scrollbar-width: none; /* for Firefox */
  overflow-y: scroll;
}

template::-webkit-scrollbar {
  display: none; /* for Chrome, Safari, and Opera */
}
</style>>
