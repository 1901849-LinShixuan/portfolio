<template>
  <div>
    <div class="main-view" :class="{ hidden: scrolledDown }">
      <div class="sider sidebar">
        <div class="holder">
          <div class="xx" role="navigation" aria-labelledby="main-nav-heading">
            <a class="listitem" href="#Intro">Intro</a>
            <a class="listitem" href="#Projects">Projects</a>
            <a class="listitem" href="#Resume">Résumé</a>
            <br />
            <div class="contact">
              <a href="mailto:yourmail@gmail.com"> linshixuana97@gmail.com</a>
              <a href="https://github.com/1901849-LinShixuan/"
                ><Fa fa="github" /> 1901849-LinShixuan</a
              >
              <a href="https://www.linkedin.com/in/nathanielin/">
                <Fa fa="linkedin" /> Nathaniel Lin Shixuan
              </a>
            </div>
          </div>
        </div>
      </div>
      <div class="main">
        <section id="intro">
          <div class="txt">
            <h1>
              Hi, I am Nathaniel Lin.
              <br />
              An aspiring UI/UX FrontEnd Developer
            </h1>
            <br />
            <a href="#Intro">About Me <Fa fa="arrow-down" /></a>
          </div>
        </section>
        <section id="Intro" aria-labelledby="intro-heading">
          <h2 id="intro-heading">About Me</h2>
          <span>
            Graduated with a BSc with Honours in Computing Science jointly
            offered by Singapore Insitute of Technology & the University of
            Glasgow. My interest lies in UI/UX design, mobile and web
            development, and data visualization.
          </span>
        </section>
        <section id="Projects" aria-labelledby="Projects-heading">
          <h2 id="Projects-heading">Projects</h2>
          <div class="cards">
            <div class="card-col">
              <Card :item="projects[0]" :txt="select" />
              <Card :item="projects[1]" :txt="select" />
            </div>
            <div class="card-col">
              <Card :item="projects[2]" :txt="select" />
              <Card :item="projects[3]" :txt="select" />
            </div>
          </div>
        </section>
        <section id="Erfahrungen"></section>
        <section id="Resume" aria-labelledby="Resume-heading">
          <h2 id="Resume-heading">Résumé</h2>
          <div class="Resume">
            <img
              src="./nathaniel_cv-1.png"
              alt="Updated as at 14 Aug 22"
              style="
                width: 654px;
                border: 7px solid blanchedalmond;
                border-radius: 5px;
              "
            />
          </div>
          <br />
          <Fa fa="file-pdf" />
          <a href="./nathaniel_cv.pdf" download> NathanielResume_14Aug22</a>
        </section>
      </div>
    </div>
    <PopOver :selected="selected" :closeWindow="closePopOver" />
  </div>
</template>

<script>
import Card from './globals/Card.vue';
import Fa from './globals/Fa.vue';
import PopOver from './PopOver.vue';

export default {
  components: {
    Card,
    Fa,
    PopOver,
  },
  data: () => ({
    projects: [
      {
        id: 0,
        images: [
          {
            img: './images/melody.gif',
          },
          {
            img: './images/melody.png',
          },
        ],
        titel: 'GUTS Hackathon - Melody App',
        tags: ['Kotlin', 'Adobe Illustrator'],
        demo: 'https://www.youtube.com/watch?v=gVzpLzOltyI',
        source: 'https://play.google.com/store/apps/details?id=com.team08.cs',
      },
      {
        id: 1,
        images: [
          {
            img: './images/pinkofhealth.gif',
          },
          {
            img: './images/pinkofhealth.png',
          },
        ],
        titel: 'Healthcare Mobile Application',
        tags: ['Kotlin', 'Google Firebase'],
        demo: 'https://youtu.be/05Uf4f-kjdM',
        source: '',
      },
      {
        id: 2,
        images: [
          {
            img: './images/hexbin-1.png',
          },
          {
            img: './images/hexbin-cartogram.png',
          },
        ],
        titel: 'Data Visualization on Covid-19 Cases',
        tags: ['LeafletJs', 'TurfJs'],
        demo: 'https://1901849-linshixuan.github.io/HexBinMap/',
        source: 'https://github.com/1901849-LinShixuan/HexBinMap',
      },
      {
        id: 3,
        images: [
          {
            img: './images/lucene.gif',
          },
          {
            img: './images/Lucene.png',
          },
        ],
        titel: 'Lucene Search Engine',
        tags: ['Apache Lucene', 'NodeJS'],
        demo: 'https://youtu.be/5hpFFes38Zw',
        source: '',
      },
    ],
    selected: null,
  }),
  mounted() {
    window.onscroll = this.lodash.debounce(this.scrollcalc, 5);
    this.scrollcalc();
    let anchorlinks = document.querySelectorAll('a[href^="#"]');

    for (let item of anchorlinks) {
      item.addEventListener('click', (e) => {
        let hashval = item.getAttribute('href');
        let target = document.querySelector(hashval);
        target.scrollIntoView({
          behavior: 'smooth',
          block: 'start',
        });
        history.pushState(null, null, hashval);
        e.preventDefault();
      });
    }
  },
  methods: {
    select: function (id) {
      this.selected = this.projects.find((x) => x.id === id);
    },
    closePopOver() {
      this.selected = null;
    },
    scrollcalc() {
      let mainNavLinks = document.querySelectorAll('.xx a');
      let fromTop = document.documentElement.scrollTop;
      let navbarHeight = 200;

      mainNavLinks.forEach((link) => {
        if (link.hash == '') return;

        let section = document.querySelector(link.hash);
        if (section == null) return;
        if (
          section.offsetTop <= fromTop + window.innerHeight &&
          section.offsetTop + section.offsetHeight > fromTop + navbarHeight
        ) {
          link.classList.add('current');
          let allCurrents = document.querySelectorAll('.current');
          let allFirsts = document.querySelector('.first');
          if (allFirsts != null) {
            allFirsts.classList.remove('first');
          }
          allCurrents[0].classList.add('first');
        } else {
          link.classList.remove('current');
        }
      });
    },
  },
  props: {
    scrolledDown: Boolean,
  },
};
</script>

<style lang="scss" scoped>
#intro {
  .txt {
    a {
      display: none;
      text-decoration: none;
      color: black;
    }
  }
}
@media screen and (max-width: 680px) {
  .cards {
    display: block !important;
  }
  .card {
    width: 100% !important;
    height: 33rem !important;
  }
  #intro {
    .txt {
      a {
        display: hidden;
      }
    }
  }
  .hidden {
    #intro {
      .txt {
        a {
          display: block;
        }
      }
    }
  }
  .cont {
    grid-template-areas:
      'datum'
      'extra'
      'titel'
      'ort'
      'txt' !important;
    grid-template-columns: 100% !important;
  }
  .txt h1 {
    font-size: 7vw !important;
  }
}
#Kontakt,
#Resume {
  a {
    color: black;
    i {
      font-size: 0.9rem;
    }
  }
  a:hover {
    color: hsl(0deg 0% 63%);
  }
}
.bildungsweg,
.Resume {
  h3 {
    font-size: 0.9rem;
    color: white;
  }
  cursor: default;
}
.cont {
  display: grid;
  grid-template-areas:
    'datum titel'
    'extra ort'
    '. txt';
  grid-template-columns: 11rem 370px;
  gap: 0rem 1rem;
  margin-bottom: 1.3rem;
  span:nth-child(1) {
    grid-area: datum;
    font-weight: 600;
    font-size: 0.9rem;
    color: hsl(0deg 0% 63%);
    letter-spacing: -0.02rem;
  }
  span:nth-child(2) {
    grid-area: extra;
    font-size: 0.87rem;
    color: hsl(0deg 0% 63%);
    letter-spacing: -0.02rem;
  }
  span:nth-child(3) {
    grid-area: titel;
  }
  span:nth-child(4) {
    grid-area: ort;
    font-size: 0.9rem;
    color: hsl(0deg 0% 63%);
  }
  span:nth-child(5) {
    grid-area: txt;
    font-size: 0.9rem;
    color: hsl(0deg 0% 63%);
  }
}

.contact {
  // margin: 2rem 0rem;
  display: flex;
  flex-flow: column;
  gap: 1.05rem;
  width: 100%;
  transition: opacity 0.3s;
  a {
    text-decoration: none;
    color: var(--txt-med);
    padding: 0rem 1.5rem;
  }
}
.contact {
  a:hover {
    color: black;
  }
}
#Intro {
  a {
    color: var(--accent-1);
    text-decoration: none;
    i {
      margin-left: 0.4rem;
    }
  }
}
section {
  padding: 2.5rem 0rem;
  &:empty {
    display: none;
  }
  span {
    display: block;
    max-width: 550px;
    text-align: justify;
  }
}
.mainitem-active {
  border-radius: 6px;
  background: hsl(220 100% 71% / 0.11);
  color: hsl(220 100% 53% / 1) !important;
  margin-bottom: 0.3rem;
}
.title {
  font-size: 12px !important;
  font-weight: 700 !important;
  margin: 0.2em 0em 1rem 0rem;
  text-transform: capitalize;
  color: #b2b2b2;
  text-transform: uppercase;
  letter-spacing: 0.02rem;
  width: 100%;
  text-align: center;
}
.xx {
  display: flex;
  flex-flow: column;
  align-items: self-end;
  margin-top: 44px;
  gap: 1.05rem;
  a {
    transition: min-width 0.3s, border 0.3s, padding 0.3s, box-shadow 0.3s,
      background 0.15s;
    width: fit-content;
    min-width: 210px;
    max-width: -webkit-fill-available;
  }
}
.listitem:nth-child(1).first {
  background: lightgrey;
}
.listitem:nth-child(2).first {
  background: var(--accent-1);
}
.listitem:nth-child(3).first {
  background: var(--accent-2);
}
.listitem:nth-child(4).first {
  background: var(--accent-3);
}
.listitem:nth-child(5).first {
  background: var(--accent-4);
}
.listitem:nth-child(6).first {
  background: var(--accent-5);
}
.listitem:nth-child(7).first {
  background: var(--accent-6);
}
.listitem:hover {
  background-color: hsla(0, 0%, 80%, 0.15);
}
.listitem {
  text-decoration: none;
  display: block;
  padding: 0.75rem 1.8rem;
  margin-right: 1rem;
  color: black;
  font-size: 0.95em;
  cursor: pointer;
  transition: border 0.3s, padding 0.3s, box-shadow 0.3s, background 0.15s;
  border-left: 2px solid transparent;
  font-weight: 500;
  border-radius: 0.4rem;
}
.mainitem {
  padding: 0.5rem 0.5rem;
}
.current {
  border-left: 6px solid #ffffff1c;
  // box-shadow: 0px 0px 0px 0px black;
}
.first {
  color: black;
  color: black !important;
  padding-left: 2rem;
  font-weight: 600;
  transform-origin: left;
  animation: pop 0.25s ease-out;
}
@keyframes pop {
  35% {
    transform: scale(1.05);
  }
  75% {
    transform: scale(0.96);
  }
  100% {
    transform: scale(1);
  }
}
</style>

<style lang="scss" scoped>
.card-col:nth-child(2) {
  margin-top: 5rem;
}
.cards {
  display: flex;
  gap: 1.7rem;
}
.card-col {
  display: flex;
  flex-flow: column;
  gap: 1.7rem;
}

.sidebar,
.sideoptions {
  transition: width 0.3s;
}
@media screen and (max-width: 1300px) {
  .main-view {
    grid-template: 'siderbar main main';
  }
  .sideoptions {
    display: none;
  }
}
@media screen and (max-width: 1023px) {
  .main-view {
    grid-template: 'main main main' !important;
    grid-template-columns: 1fr !important;
    width: auto !important;
  }
  .sidebar {
    display: none;
  }
}

.holder {
  scrollbar-color: #bebebe transparent;
  scrollbar-width: thin;
}
.holder:hover {
  scrollbar-color: #bebebe #f2f2f2;

  scrollbar-width: revert !important;
}

.holder::-webkit-scrollbar {
  width: 15px;
  padding: 10px;
}

.holder::-webkit-scrollbar-thumb {
  border-radius: 10px;
  /* background-color: #bebebe; */
  border: 5px solid transparent;
  background-clip: content-box;
}

.sider:hover .holder::-webkit-scrollbar {
  width: 15px;
}

.sider:hover .holder::-webkit-scrollbar-track {
  border-radius: 10px;
}

.sider:hover .holder::-webkit-scrollbar-thumb {
  border: 0;
  border-radius: 10px;
}

.sider:hover .holder::-webkit-scrollbar-thumb:hover {
  background: #818b99;
}
.sider {
  height: 100%;
  width: 310px;
}
.holder {
  padding: 1rem;
  position: -webkit-sticky;
  position: sticky;
  top: 60px;
  height: calc(100vh - 90px);
  overflow-y: auto;
}
.sidebar {
  justify-self: right;
}

.link .fas {
  font-size: 0.8rem;
}

.filters > .text {
  padding: 0.5em 0em;
  display: block;
}
.filters > .text > input {
  width: 125px;
  border: 0;
  background: 0;
  margin: 0rem 0.3rem;
  border-bottom: 1px solid gray;
}
.filters {
  margin: 2rem 0rem;
}

h2 {
  font-size: 1rem;
  color: var(--txt-med);
  cursor: default;
}
.main-view {
  display: grid;
  grid-template: 'siderbar main';
  grid-template-columns: 1fr minmax(600px, 770px);
  width: fit-content;
  margin-left: auto;
  margin-right: auto;
  z-index: 100;
}
div > .main {
  max-width: 1000px;
  margin: auto;
  box-sizing: border-box;
  line-height: 1.6;
  color: var(--txt);
  padding: 0rem 1.5rem 1.5rem;
  width: 100%;
  z-index: 100;
}
</style>
<style scoped lang="scss">
.txt h1 {
  font-size: 3rem;
  margin: 0.2rem 0;
  margin-bottom: 12rem;
  line-height: 1.3;
  max-width: 600px;
}
.main-view {
  transition: background 0.3s;
  section {
    transition: opacity 0.3s;
  }
}

.main-view,
.main-view {
  .main .holder,
  .sider {
    transition: background 0.3s;
  }
}
.hidden {
  .xx {
    a {
      transition: min-width 0.3s;
      min-width: 0px;
      width: fit-content;
    }

    .title {
      opacity: 0;
    }
    .listitem {
      border: 0;
      background: lightgrey;
      color: black;
    }
    .listitem:nth-child(2) {
      background: var(--accent-1);
    }
    .listitem:nth-child(3) {
      background: var(--accent-2);
    }
    .listitem:nth-child(4) {
      background: var(--accent-3);
    }
    .listitem:nth-child(5) {
      background: var(--accent-4);
    }
    .listitem:nth-child(6) {
      background: var(--accent-5);
    }
    .listitem:nth-child(7) {
      background: var(--accent-6);
    }
    .listitem:hover {
      background: #fbfbfb;
    }
  }
  .contact,
  section {
    opacity: 0;
  }
  .main,
  .holder,
  .sider {
    background: transparent !important;
  }
  background: transparent !important;
  box-shadow: unset !important;
}
#intro {
  opacity: 100;
}
</style>
