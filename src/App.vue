<template>
  <header id="banner">
    <div class="wrap">
      <div class="container">
        <div class="box">
          <div class="title">
            <span class="block"></span>
            <h1>ALEKSEY PROTOPOPOV<span></span></h1>
          </div>
          
          <div class="role">
            <div class="block"></div>
            <p>Data visualization & Frontend Dev</p>
          </div>
        </div>
      </div>
    </div>
  </header>
  
  <main>
    <div>
      <div class="portfolio wrap">
        <div class="portfolio-container col-lg-4 col-md-6" v-for="item in projects" :key="item.name">
          <a class="portfolio-box" :href="item.href" target="_blank">
            <img
              class="img-fluid"
              :src="item.image"
              :alt="item.name"
            />
            <div class="portfolio-box-caption">
              <div class="portfolio-box-caption-content">
                {{ item.title }}
              </div>
            </div>
          </a>
        </div>
      </div>
    </div>
  </main>
  
  <footer id="landing-footer" class="wrap">
    <div class="row text-center">
      <div class="col-12">
        <a href="https://github.com/ProtopopovAleksey" target="_blank">
          <i class="bi bi-github icon"></i>
        </a>
        <a href="https://www.linkedin.com/in/alexey-protopopov-a05346180/" target="_blank">
          <i class="bi bi-linkedin icon"></i>
        </a>
        <a href="mailto:alekseiii96@gmail.com?Subject=Data%20Visualization">
          <i class="bi bi-envelope-fill icon"></i>
        </a>
      </div>
    </div>
  </footer>
</template>

<script>
  
  export default {
    name: 'App',
    components: {},
    data() {
      return {
        projects: [
          {
            title: 'European tourism in bar race format',
            image: 'images/d3-bar-race-chart.PNG',
            href: 'https://protopopovaleksey.github.io/d3-bar-race-chart'
          },
          {
            title: 'Data story about US police shooting',
            image: 'images/d3-story.PNG',
            href: 'https://protopopovaleksey.github.io/d3-data-story'
          },
          {
            title: 'D3 bubbles chart with text wrapping',
            image: 'images/d3-bubbles-chart.PNG',
            href: 'https://protopopovaleksey.github.io/d3-bubbles-chart'
          },
          {
            title: 'D3 radial chart with custom styling',
            image: 'images/d3-radial-chart.PNG',
            href: 'https://protopopovaleksey.github.io/d3-radial-chart'
          },
          {
            title: 'D3 line chart with custom styling',
            image: 'images/d3-line-chart.PNG',
            href: 'https://protopopovaleksey.github.io/d3-linear-chart'
          },
          {
            title: 'Visualization of geological data',
            image: 'images/d3-core-visualization.PNG',
            href: 'https://protopopovaleksey.github.io/core-visualization/'
          },
        ]
      }
    },
    mounted() {
      // Image hover
      var counter = 0;
      var refreshRate = 10;
      
      var imageTransformFriction = 1 / 10;
      
      // Throttle updateImageTransform
      var isTimeToUpdate = function () {
        return counter++ % refreshRate === 0;
      };
      
      var onMouseEnterHandler = function (event) {
        mouse.setOrigin(this);
        var img = this.getElementsByTagName("img")[0];
        updateImageTransform.call(img, event);
      };
      
      var onMouseMoveHandler = function (event) {
        if (isTimeToUpdate()) {
          var img = this.getElementsByTagName("img")[0];
          updateImageTransform.call(img, event);
        }
      };
      
      var onMouseLeaveHandler = function (event) {
        var img = this.getElementsByTagName("img")[0];
        resetImageTransform.call(img, event);
      };
      
      var updateImageTransform = function (event) {
        mouse.updatePosition(event);
        var x = -mouse.x * imageTransformFriction;
        var y = -mouse.y * imageTransformFriction;
        var transform = "translate(" + x + "px," + y + "px)scale(1.1)";
        this.style.transform = transform;
        this.style.webkitTransform = transform;
        this.style.mozTranform - transform;
      };
      
      var resetImageTransform = function () {
        var transform = "scale(1.1)";
        this.style.transform = transform;
        this.style.webkitTransform = transform;
        this.style.mozTranform - transform;
      };
      
      var mouse = {
        _x: 0,
        _y: 0,
        x: 0,
        y: 0,
        updatePosition: function (event) {
          var e = event || window.event;
          this.x = e.pageX - this._x;
          this.y = e.pageY - this._y;
        },
        setOrigin: function (el) {
          var domRect = el.getBoundingClientRect();
          this._x = window.pageXOffset + domRect.left + domRect.width / 2;
          this._y = window.pageYOffset + domRect.top + domRect.height / 2;
        }
      };
      
      var portfolioItems = document.getElementsByClassName("portfolio-container");
      console.log(portfolioItems)
      Array.prototype.forEach.call(portfolioItems, function (el) {
        el.onmouseenter = onMouseEnterHandler;
        el.onmousemove = onMouseMoveHandler;
        el.onmouseleave = onMouseLeaveHandler;
      });
    }
  }
</script>

<style lang="scss">
  @import url('https://fonts.googleapis.com/css?family=Lato:300,400|Poppins:300,400,800&display=swap');
  @import url('./styles/keyframes.scss');
  
  * {
    margin: 0;
    padding: 0;
  }
  
  body, html {
    background: #232323;
  }
  
  .portfolio {
    display: flex;
    flex-direction: row;
    flex-wrap: wrap;
    margin: 0 auto;
    
    .portfolio-container {
      padding: 12px;
      
      .portfolio-box {
        position: relative;
        display: block;
        overflow: hidden;
        box-shadow: 2px 2px 25px rgba(0, 0, 0, 0.2);
        padding-bottom: 62.5%;
        height: 0;
        
        
        img {
          transform: scale(1.1);
          transition: 0.5s ease;
          
          max-width: 100%;
          height: auto;
        }
        
        .portfolio-box-caption {
          position: absolute;
          bottom: 0;
          display: block;
          width: 100%;
          height: 100%;
          text-align: center;
          opacity: 0;
          -webkit-transition: 0.2s ease;
          -moz-transition: 0.2s ease;
          transition: 0.2s ease;
        }
        
        &:focus {
          outline: 0;
        }
        
        &:hover {
          
          .portfolio-box-caption {
            opacity: 1;
            font-family: "Open Sans", sans-serif, Arial, Helvetica;
            font-size: 18px;
            color: #111;
            background: rgba(255, 255, 255, 0.1);
          }
        }
      }
      
      .portfolio-box
      .portfolio-box-caption
      .portfolio-box-caption-content {
        position: absolute;
        top: 50%;
        width: 100%;
        transform: translateY(-50%);
        text-align: center;
        font-weight: bold;
        color: #111;
        text-shadow: -1px -1px 0 #fff, 1px -1px 0 #fff, -1px 1px 0 #fff,
        1px 1px 0 #fff;
        pointer-events: none;
      }
    }
  }
  
  .container {
    width: 100%;
    display: flex;
    justify-content: flex-start;
    align-items: center;
    
    .box {
      width: 450px;
      height: 250px;
      position: relative;
      display: flex;
      justify-content: center;
      flex-direction: column;
      
      .title {
        width: 100%;
        position: relative;
        display: flex;
        align-items: center;
        height: 32px;
        
        .block {
          width: 0%;
          height: inherit;
          background: #feb410;
          position: absolute;
          animation: mainBlock 2s cubic-bezier(.74, .06, .4, .92) forwards;
          display: flex;
        }
        
        h1 {
          font-family: 'Poppins';
          color: #fff;
          font-size: 32px;
          -webkit-animation: mainFadeIn 2s forwards;
          -o-animation: mainFadeIn 2s forwards;
          animation: mainFadeIn 2s forwards;
          animation-delay: 1.6s;
          opacity: 0;
          display: flex;
          align-items: baseline;
          position: relative;
          margin-bottom: 0;
          
          span {
            width: 0px;
            height: 0px;
            -webkit-border-radius: 50%;
            -moz-border-radius: 50%;
            border-radius: 50%;
            
            background: #feb410;
            -webkit-animation: load 0.6s cubic-bezier(.74, .06, .4, .92) forwards;
            animation: popIn 0.8s cubic-bezier(.74, .06, .4, .92) forwards;
            animation-delay: 2s;
            margin-left: 5px;
            margin-top: -10px;
            position: absolute;
            bottom: 13px;
            right: -12px;
            
          }
        }
      }
      
      .role {
        width: 100%;
        position: relative;
        display: flex;
        align-items: center;
        height: 14px;
        
        .block {
          width: 0%;
          height: inherit;
          background: #e91e63;
          position: absolute;
          animation: secBlock 2s cubic-bezier(.74, .06, .4, .92) forwards;
          animation-delay: 2s;
          display: flex;
        }
        
        p {
          animation: secFadeIn 2s forwards;
          animation-delay: 3.2s;
          opacity: 0;
          font-weight: 400;
          font-family: 'Lato';
          color: #fff;
          font-size: 12px;
          text-transform: uppercase;
          letter-spacing: 5px;
          margin-bottom: 0;
        }
      }
      
      @media (max-width: 440px) {
        .role {
          margin-top: 5px;
        }
      }
      
      @media (max-width: 394px) {
        .role {
          margin-top: 25px;
        }
        .title {
          h1 {
            span {
              left: 220px;
            }
          }
        }
      }
    }
  }
  
  #app {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
    margin-top: 60px;
  }
  
  #banner {
    text-align: left;
  }
  
  .wrap {
    max-width: 1140px;
    margin: 0 auto;
  }
  
  /*Button*/
  .button {
    font-size: 16px;
    margin: 35px 0;
    padding: 11px 16px;
    transition: all 0.3s ease;
    display: inline-block;
    border: 3px solid #2c3e50;
    text-decoration: none;
    color: #2c3e50;
    
    &:hover {
      color: #feb410;
      border-color: #feb410;
    }
  }
  
  #banner .section-heading:before,
  #banner .section-heading:after,
  footer:before {
    content: "";
    display: block;
    width: 30px;
    height: 5px;
    margin-top: 30px;
    background: #feb410;
  }
  
  footer {
    margin: 0 auto;
    
    &:before {
      margin: 30px auto 25px auto;
    }
  }
  
  #landing-footer,
  #landing-footer p,
  #landing-footer a {
    font-family: "Open Sans", sans-serif, Arial, Helvetica;
    font-size: 12px;
    font-weight: normal;
    color: #999;
    
    .icon {
      font-size: 1.5rem;
      margin-right: 15px;
    }
  }

</style>
