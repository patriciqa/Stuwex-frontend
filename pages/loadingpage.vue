<template>
   <body>
       <div class="welcome-page" id="welcome-page">
                <div class="welcome-content">
                    <section id="kreis">
                        <svg class="progress-circle" width="260" height="260">
                            <path d="M130,16.8c62.5,0,113.2,50.6,113.2,113.2S192.5,243.2,130,243.2S16.8,192.5,16.8,130S67.5,16.8,130,16.8z" />
                        </svg>
                        <svg class="progress-circle-dashed" width="260" height="260">
                            <path d="M130,16.8c62.5,0,113.2,50.6,113.2,113.2S192.5,243.2,130,243.2S16.8,192.5,16.8,130S67.5,16.8,130,16.8z" />
                        </svg>
                    </section>
                    <section id="welcome-text">
                        <p class="welcome-text welcome-text-heading">Grosssiedlungen in Pressebildern</p>
                        <p class="welcome-text welcome-text-subheading">Hoffnungsträger oder Symbol der Wachstumskritik?</p>
                    </section>
                </div>
            </div>
   </body>
</template>



<script>
export default {
    mounted(){
         gsap.registerPlugin(ScrollTrigger);

        var path = document.getElementsByTagName("path");
        var pathLength = path[0].getTotalLength();
        console.log(pathLength);

        var currentPathLength = pathLength;
        var step=2;
        var percent=0;

            function doAnim() {
                path[0].style.strokeDashoffset = pathLength * (1-percent);
            }


        gsap.to('#kreis', {
            scrollTrigger:{
                trigger: "#welcome-page",
                onUpdate: (self) => {
                    // console.log(self.progress)
                    percent =self.progress;
                    doAnim()
                },
                markers: true,
                start: "top 0%",
                end: "bottom 100%"
            }
        })
    }
}
</script>



<style scoped>
    body{
        background-color:var(--black);
        color: var(--white);
    }

    .welcome-text{
        text-align: center;
    }

    .welcome-text-heading{
        font-family: "IBM Plex Sans";
        font-weight: 600;
        font-size: 4rem;
    }

    .welcome-text-subheading{
        font-size: 1.5rem;
    }
  
  /* Scrollbar fix */
        template{
            -ms-overflow-style: none; /* for Internet Explorer, Edge */
            scrollbar-width: none; /* for Firefox */
            overflow-y: scroll; 
        }

        template::-webkit-scrollbar {
           display: none; /* for Chrome, Safari, and Opera */
        }
 
 .welcome-page{
            display: flex;
            flex-direction: column;
            height: 150vh;
            align-items: center;
            justify-content: center;
        }

        .welcome-content{
            position: fixed;
            margin: 5vh 0;
            height: 100%;
        }

        svg{
            /* transform-origin: 50 50; */
            transform: scale(2.5); 
        }

        #kreis{
            display: grid;
            grid-template-rows: 1fr;
            grid-template-columns: 1fr;
            grid-template-areas:
            "centerfix"
            "centerfix";
            justify-content: center;
            margin-bottom: 10vh;
            
        }
        #kreis svg{
            grid-area: centerfix;
            margin: 0 auto;
            
        }

        path{
            stroke: #fff;
            fill: none;
            margin: 0 auto;
            justify-content: center;
            position: sticky;
        }

        .progress-circle path {
            stroke-dasharray: 711;
            stroke-dashoffset: 0;  
            stroke-width: 2;
        }

        .progress-circle-dashed{
            stroke-dasharray: 4 6;
            stroke-width: 1;
            z-index: -1;
        }

</style>>
