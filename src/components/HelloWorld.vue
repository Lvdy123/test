<template>
  <div class="hello">
    <div class="banner">
      <ul class="clearfix">
        <li>
          <a href="#">
            <img src="../common/images/l8.jpg" alt>
          </a>
        </li>
        <li>
          <a href="#">
            <img src="../common/images/l1.jpg" alt>
          </a>
        </li>
        <li>
          <a href="#">
            <img src="../common/images/l2.jpg" alt>
          </a>
        </li>
        <li>
          <a href="#">
            <img src="../common/images/l3.jpg" alt>
          </a>
        </li>
        <li>
          <a href="#">
            <img src="../common/images/l4.jpg" alt>
          </a>
        </li>
        <li>
          <a href="#">
            <img src="../common/images/l5.jpg" alt>
          </a>
        </li>
        <li>
          <a href="#">
            <img src="../common/images/l6.jpg" alt>
          </a>
        </li>
        <li>
          <a href="#">
            <img src="../common/images/l7.jpg" alt>
          </a>
        </li>
        <li>
          <a href="#">
            <img src="../common/images/l8.jpg" alt>
          </a>
        </li>
        <li>
          <a href="#">
            <img src="../common/images/l1.jpg" alt>
          </a>
        </li>
      </ul>
      <ul>
        <li class="now"></li>
        <li></li>
        <li></li>
        <li></li>
        <li></li>
        <li></li>
        <li></li>
        <li></li>
      </ul>
    </div>
  </div>
</template>
<script>
export default {
  name: 'HelloWorld',
  data() {
    return {};
  },
  computed: {},
  methods: {
    mySwiper: function(){
      
        var banner = document.querySelector('.banner');
        
        var baWidth = banner.offsetWidth;
        
        var imageBox = banner.children[0];

        var pointBox = banner.children[1];
        
        var points = pointBox.querySelectorAll('li');
        
        var addTransition = function () {
            imageBox.style.transition = 'all .3s ease';
            
            imageBox.style.webkitTransition = 'all .3s ease';
        };
        var addTranslate = function (x) {
            imageBox.style.transform = 'translateX(' + x + 'px)';
            imageBox.style.webkitTransform = 'translateX(' + x + 'px)';
        };
        var clearTransition = function () {
            imageBox.style.transition = 'none';
            imageBox.style.webkitTransition = 'none';
        };
        var index = 1;
        var timer = setInterval(function () {
            index++;
            addTransition();
            addTranslate(-baWidth * index);
        }, 1000);

        imageBox.addEventListener('webkitTransitionEnd', function () {
            if (index >= 9) {
                index = 1;

                clearTransition();
                
                addTranslate(-baWidth * index);
            } else if (index == 0) {
                index = 8;

                clearTransition();

                addTranslate(-baWidth * index);
            }
            setPoint();
        });

        function setPoint() {
            for (var i = 0; i < points.length; i++) {
                points[i].className = '';
            }
            points[index - 1].className = 'now';
        }
        var startX = 0, 
            moveX = 0, 
            distanceX = 0, 
            ISMOVE = false; 
        imageBox.addEventListener('touchstart', function (e) {
            e.preventDefault();
            clearInterval(timer);
            timer = null;
            startX = e.touches[0].pageX;
        });
        imageBox.addEventListener('touchmove', function (e) {
            e.preventDefault();
            ISMOVE = true;
            moveX = e.touches[0].pageX;
            distanceX = moveX - startX;
            clearTransition();
            addTranslate(-index * baWidth + distanceX);
        });
        imageBox.addEventListener('touchend', function (e) {
            e.preventDefault();
            if (!ISMOVE) {
                return;
            }
            if (Math.abs(distanceX) > baWidth / 3) {
                if (distanceX > 0) {
                    index--;
                } else {
                    index++;
                }
                addTransition();
                addTranslate(-index * baWidth);
            } else {
                addTransition();
                addTranslate(-index * baWidth);
            }
            startX = 0,
                moveX = 0,
                distanceX = 0,
                ISMOVE = false;
            timer = setInterval(function () {
                index++;
                addTransition();
                addTranslate(-index * baWidth);
            }, 1000);
        });
    }
  },
  watch: {},
  components: {},
  mounted:function(){
    this.mySwiper();
  },
};
</script>

<style scoped>
ul,
ol {
  list-style: none;
  padding: 0;
  margin: 0;
}

.clearfix::before,
.clearfix::after {
  content: "";
  height: 0;
  line-height: 0;
  display: block;
  visibility: hidden;
  clear: both;
}

.banner {
  width: 100%;
  position: relative;
  overflow: hidden;
}

.banner > ul:first-child {
  width: 1000%;
  -webkit-transform: translateX(-10%);
  transform: translateX(-10%);
}

.banner > ul:first-child > li {
  width: 10%;
  float: left;
}

.banner > ul:first-child > li > a {
  width: 100%;
  display: block;
}

.banner > ul:first-child > li > a > img {
  width: 100%;
  display: block;
}

.banner > ul:last-child {
  width: 134px;
  height: 8px;
  position: absolute;
  bottom: 6px;
  left: 50%;
  margin-left: -67px;
}

.banner > ul:last-child > li {
  width: 6px;
  height: 6px;
  float: left;
  border-radius: 4px;
  border: 1px solid #fff;
  margin-left: 10px;
}

.banner > ul:last-child > li.now {
  background: #fff;
}

.banner > ul:last-child > li:nth-child(1) {
  margin-left: 0;
}
</style>
