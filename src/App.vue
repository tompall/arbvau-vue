
<template>

  <div id="app">
    <div class="full-window-w-bg" :style="{ backgroundImage: 'url(' + activePage.background_img + ')' }"></div>
    <ul class="nav">
      <li v-for="(item,index) in pages"><a @click="changeView(index)" :href="'#'+item.url"><img :src="item.icon"/></a></li>
    </ul>
    <div class="imagegrid-wrapper">
      <ul class="images">
        <img v-for="image in activePage.images" :src="image" :style="{ width:getRandomInt(20,50)+'%'}" />
      </ul>
    </div>
    <div class="video-embed">
      <div class="embed-container">
        <iframe :src="activePage.video_url" width="500" height="400" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen ></iframe>
      </div>
    </div>
    <div class="infopanel" v-if="infoPanelState" @click="infoPanelState = !infoPanelState">
      <h2>{{activePage.description}}</h2>
    </div>
    <div class="title" @click="infoPanelState = !infoPanelState">
      <h1>{{activePage.title}}</h1>
    </div>
    <div class="infobutton" @click="infoPanelState = !infoPanelState">
        <h1>info</h1>
    </div>
  </div>
</template>

<script>
//BACKGROUNDS
import zetbg from "./assets/bg/zetbg.jpg"
import spambg from "./assets/bg/spambg.jpg"
import atlbg from "./assets/bg/atlbg.jpg"
import bolicbg from "./assets/bg/bolicbg.jpg"
import ritesbg from "./assets/bg/ritesbg.jpg"
import ghostbg from "./assets/bg/ghostbg.jpg"
import rnbg from "./assets/bg/rnbg.jpg"
import legendabg from "./assets/bg/legendabg.jpg"
import pfichtlybg from "./assets/bg/pfichtlybg.jpg"
import ujbalabg from "./assets/bg/ujbalabg.jpg"
//ICONS
import zeticon from "./assets/icons/zeticon.png"
import spamicon from "./assets/icons/spamicon.png"
import atlicon from "./assets/icons/atlicon.png"
import bolicicon from "./assets/icons/bolicicon.png"
import ritesicon from "./assets/icons/ritesicon.png"
import ghosticon from "./assets/icons/ghosticon.png"
import rnicon from "./assets/icons/rnicon.png"
import legendaicon from "./assets/icons/legendaicon.png"
import pfichtlyicon from "./assets/icons/pfichtlyicon.png"
import ujbalaicon from "./assets/icons/ujbalaicon.png"
//images
import zet1 from "./assets/zet/img/zet1.jpg"
import zet2 from "./assets/zet/img/zet2.jpg"
import zet3 from "./assets/zet/img/zet3.jpg"
import zet4 from "./assets/zet/img/zet4.jpg"
import zet5 from "./assets/zet/img/zet5.jpg"

import spam1 from "./assets/ssp/img/spam0.jpg"
import spam2 from "./assets/ssp/img/spam1.jpg"
import spam3 from "./assets/ssp/img/spam3.jpg"
import spam4 from "./assets/ssp/img/spam4.jpg"
import spam5 from "./assets/ssp/img/spam7.jpg"
import spam6 from "./assets/ssp/img/spam11.jpg"
import spam7 from "./assets/ssp/img/spam13.jpg"

import atl1 from "./assets/atl/img/atl1.png"
import atl2 from "./assets/atl/img/atl2.png"
import atl3 from "./assets/atl/img/atl3.png"
import atl4 from "./assets/atl/img/atl4.png"
import atl5 from "./assets/atl/img/atl5.png"

import bolic1 from "./assets/bolic/img/bolic1.jpg"
import bolic2 from "./assets/bolic/img/bolic2.jpg"
import bolic3 from "./assets/bolic/img/bolic3.jpg"
import bolic4 from "./assets/bolic/img/bolic4.jpg"
import bolic5 from "./assets/bolic/img/bolic5.jpg"
import bolic6 from "./assets/bolic/img/bolic5.jpg"

import ujb1 from "./assets/ujb/img/ub1.jpg"
import ujb2 from "./assets/ujb/img/ub2.jpg"
import ujb3 from "./assets/ujb/img/ub3.jpg"
import ujb4 from "./assets/ujb/img/ub4.jpg"

import rites1 from "./assets/rites/img/r0.jpg"
import rites2 from "./assets/rites/img/r3.png"
import rites3 from "./assets/rites/img/r4.png"
import rites4 from "./assets/rites/img/r5.jpg"
import rites5 from "./assets/rites/img/r6.jpg"
import rites6 from "./assets/rites/img/r7.jpg"
import rites7 from "./assets/rites/img/r8.jpg"

import rn1 from "./assets/rn/img/rn1.jpg"
import rn2 from "./assets/rn/img/rn2.jpg"
import rn3 from "./assets/rn/img/rn3.jpg"
import rn4 from "./assets/rn/img/rn4.jpg"
import rn5 from "./assets/rn/img/rn5.jpg"
import rn6 from "./assets/rn/img/rn6.jpg"

import pfi1 from "./assets/pfi/img/pfi1.jpg"
import pfi2 from "./assets/pfi/img/pfi2.jpg"
import pfi3 from "./assets/pfi/img/pfi3.jpg"
import pfi4 from "./assets/pfi/img/pfi4.jpg"
import pfi5 from "./assets/pfi/img/pfi5.jpg"
import pfi6 from "./assets/pfi/img/pfi6.jpg"
import pfi7 from "./assets/pfi/img/pfi7.jpg"
import pfi8 from "./assets/pfi/img/pfi8.jpg"

import leg1 from "./assets/leg/img/legenda_1.jpg"
import leg2 from "./assets/leg/img/legenda_2.jpg"
import leg3 from "./assets/leg/img/legenda_3.jpg"
import leg4 from "./assets/leg/img/legenda_4.jpg"
import leg5 from "./assets/leg/img/legenda_5.jpg"
import leg6 from "./assets/leg/img/legenda_6.jpg"
import leg7 from "./assets/leg/img/legenda_7.jpg"
import leg8 from "./assets/leg/img/legenda_8.jpg"

export default {
  data () {
    return {
      pages:[{
          title:'ZET 018',
          images:[zet1,zet2,zet3,zet4,zet5],
          background_img: zetbg,
          icon:zeticon,
          description:"EXPERIMENTAL DISINTEGRATING RUNNERGAME BASED ON STUXNET VIRUS (A VIRUS THAT WAS USED TO ATTACK SEVERAL NUCLEAR POWER PLANTS)",
          url:'zet',
          video_url: '//player.vimeo.com/video/190472364?byline=0&amp;portrait=0'
      },
      {
          title:'SELFSPAMSIM 016',
          images:[spam1,spam2,spam3,spam4,spam5,spam6,spam7],
          background_img: spambg,
          icon:spamicon,
          description:"EXPERIMENTAL MODULAR NARRATIVE SIMULATION. MULTI-IDENTITY SIMULATION. SEMI-NPC AI IDENTITY OBFUSCATION",
          url:'selfspam',
          video_url: '//player.vimeo.com/video/169302558?byline=0&amp;portrait=0'
      },
      {
          title:'ATLANTIX 016',
          images:[atl1,atl2,atl3,atl4,atl5],
          background_img: atlbg,
          icon:atlicon,
          description:"VIRTUAL ENVIRONMENT DEPICTING PUBLIC INFRASTRUCTURE MODIFIED TO ACT AS A DIY SHARED POWER GRID",
          url:'atlantix',
          video_url: '//player.vimeo.com/video/155182079?byline=0&amp;portrait=0'
      },
      {
          title:'BOLIC 017',
          images:[bolic1,bolic2,bolic3,bolic4,bolic5,bolic6],
          background_img: bolicbg,
          icon:bolicicon,
          description:"BOLIC 2017. VIRTUAL WASTELAND WITH AI NPC GROUPS COLLECTING AND REDISTRIBUTING THE INDUSTRIAL GAME WASTE. IN COLLABORATION WITH IVÁN ROHONYI",
          url:'bolic',
          video_url: '//player.vimeo.com/video/208467661?byline=0&amp;portrait=0'
      },
      {
          title:'UJBALA:EXELSISDEI 017',
          images:[ujb1,ujb2,ujb3,ujb4],
          background_img: ujbalabg,
          icon:ujbalaicon,
          description:"VIRTUAL ENVIRONMENT FOR MUSIC VIDEO. FOR @dalmatadaniel LABEL",
          url:'ujbala',
          video_url: '//player.vimeo.com/video/246023986?byline=0&amp;portrait=0'
      },
      {
          title:'RITES 015',
          images:[rites1,rites2,rites3,rites4,rites5,rites6,rites7],
          background_img: ritesbg,
          icon:ritesicon,
          description:"FIRST-PERSON VR EXPLORATION GAME ABSTRACT DREAMLIKE OPEN-WORLD BASED ON AMATEUR VIDEOS FROM YOUTUBE COLLECTIVE MEMORY OF THE DIGITAL AGE R I T E S E X P E R I E N C E . C O M",
          url:'rites',
          video_url: '//player.vimeo.com/video/134035035?byline=0&amp;portrait=0'
      },
      {
          title:'GHOSTESTATE 017',
          images:[zet1,zet2,zet3,zet4,zet5],
          background_img: ghostbg,
          icon:ghosticon,
          description:"EXPERIMENTAL DISINTEGRATING RUNNERGAME BASED ON STUXNET VIRUS (A VIRUS THAT WAS USED TO ATTACK SEVERAL NUCLEAR POWER PLANTS)",
          url:'ghostestate',
          video_url: '//player.vimeo.com/video/216741635?byline=0&amp;portrait=0'
      },
      {
          title:'PFICHTLY 018',
          images:[pfi1,pfi2,pfi3,pfi4,pfi5,pfi6,pfi7,pfi8],
          background_img: pfichtlybg,
          icon:pfichtlyicon,
          description:"VIRTUAL A.I. MASCOT. CREATED FOR ANGYALFÖLD, BUDAPEST TO BE RELEASED PUBLICLY IN 2089. UNTIL THEN THE MASCOT LEARNS FROM IT'S SURROUNDINGS, LIKE GOVERMENT DOCUMENTS, POLICE VIDEOS AND HEDGE FUND TACTICS",
          url:'pfichtly',
          video_url: '//player.vimeo.com/video/249878835?byline=0&amp;portrait=1'
      },
      {
          title:'RITESNETWORK 01718',
          images:[rn1,rn2,rn3,rn4,rn5,rn6],
          background_img: rnbg,
          icon:rnicon,
          description:"INTERACTIVE POSTHUMAN LANDSCAPE WHERE THE NARRATIVE IS PRESENTED AS FUTURE-PREDICTIONS, GENERATED BY A MARKOV-CHAIN AND GOVERNED BY MULTILAYERED TIME MECHANIC",
          url:'ritesnetwork',
          video_url: '//player.vimeo.com/video/239825340?byline=0&amp;portrait=0'
      },
      {
          title:'LEGENDA 018',
          images:[leg1,leg2,leg3,leg4,leg5,leg6,leg7,leg8],
          background_img: legendabg,
          icon:legendaicon,
          description:"SELF-DRIVING CAR SIMULATOR PROCEDURAL NARRATIVE COMPUTATIONAL URBAN PROTOTYPING O B J E C T D E T E C T I O N C H A T B O T",
          url:'legenda',
          video_url: '//player.vimeo.com/video/239825340?byline=0&amp;portrait=0'
      }
    ],
    isActive: false,
    infoPanelState:false,
    icons:[spamicon,zeticon,atlicon,bolicicon,ritesicon,ghosticon],
    currentVideo: '//player.vimeo.com/video/190472364?byline=0&amp;portrait=0',
    activePage:""
  }
},
  methods:{
    changeView:function(view){
      this.activePage = this.pages[view];
    },
    getRandomInt:function (min, max) {
    return Math.floor(Math.random() * (max - min + 1)) + min;
    }
  },
  created:function(){
    this.activePage = this.pages[this.getRandomInt(0,9)];
  }
}
</script>

<style>
#app{
  position: absolute;
  width: 100%;
  height: 100%;
  left: 0;
  top: 0;
  overflow: hidden;
}
img{
  -webkit-transition: width 1s; /* Safari */
  transition: width 1s;
}
img:active{
  height: 100%;
  opacity: 0.1;
}
.full-window-w-bg{
  width: 100%;
  height: 100%;
  left:0;
  top:0;
  position: absolute;

  background-position: center;
  background-size: cover;
  z-index: -10;
}
.nav {
    list-style-type: none;
    margin: 0;
    padding: 0;
    width: 100%;
    bottom:0;
    left:0;
    background-color: rgba(100,100,100,0.5);
    position: fixed;
    height: auto;
    overflow: auto;
    text-align: center;
    border-style:solid;
    border-width: thin;
    opacity: 0.5;
    z-index: 2;
}
.nav:hover{
    opacity: 1;

}

.nav li a {
    display: block;
    float: left;
    color: #000;
    padding: 8px 16px;
    text-decoration: none;
}

.nav li a img{
  height: 100px;
  width: auto;
}

.nav li a.active {
    background-color: #4CAF50;
    color: white;
}

.nav li a:hover:not(.active) {
    border-style: dashed;
    border-radius: 200px;
    border-width: thin;
    border-color: #000;
}
.imagegrid-wrapper{
  width: 60%;
  height: 90%;
  left: 0;
  bottom: 125px;
  position: absolute;
  overflow-y:auto;
  overflow-x: hidden;
  z-index: 1;
}
.imagegrid-wrapper .images li{
  list-style: none;
  float:left;
  display: block;
}
.video-embed{
  width: 40%;
  position: absolute;
  top: 0;
  right: 0;
}
.video-embed .embed-container {
  position: relative;
  padding-bottom: 56.25%;
  height: 0;
  top:0;
  right: 0;
  overflow: hidden;
  max-width: 100%;
  height: auto;
}
.video-embed .embed-container iframe,
 .video-embed .embed-container object,
  .video-embed .embed-container embed {
    position: absolute;
    top: 0;
    right: 0;
    width: 100%;
    height: 100%;
}
h1{
  font-family: 'Times New Roman', cursive;
  font-style: normal;
  -webkit-text-fill-color: transparent;
  text-shadow: 1px 1px 10px #000;
  -webkit-text-stroke: 2px black;
  font-weight: 1000;
  font-size: 4em;
  padding: 0.2em;
  margin: 0;
}
.title{
  position: fixed;
  z-index: 4;
  width: auto;
  height: auto;
  bottom: 100px;
  right: 0;
}
.infopanel{
  position: absolute;
  width: 100%;
  height: 100%;
  left: 0;
  top:0;
  background-color: black;
  opacity: 0.9;
  z-index: 3;
  text-align: center;

}
.infopanel h2{
  color: #fff;
    padding: 20%;
}
.infobutton{
  position: fixed;
  left:0;
  top:0;
  width: auto;
  height: auto;
  padding: 1%;
  z-index: 99999999999;
}
.infobutton h1{
  -webkit-text-stroke: 1px white;
  font-size: 2em;
}
</style>
