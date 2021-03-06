<template>
  <div class="about">
    <disk-nav />
    <mobile-navbar />

    <main>
      <section class="head">
        <blockquote>välkommen!</blockquote>
        <p>
          Söker du kompetenta lärare till en yrkesutbildning, kodstuga eller
          gästföreläsning i Göteborg? IT-sektorn är under ständig förändring och
          det är viktigt att tillhandahålla den senaste kompetensen till
          framtidens utvecklare. Genom Codic Education får du tillgång till
          pedagogisk och kompetent personal som passar just din
          utbildningsmodell.
        </p>
      </section>
      <section class="about-us">
        <h2>vilka är vi?</h2>
        <p>
          <span>Codic Education</span> har knoppats av från Codic Consulting och
          besitter samma tekniska kompetens och rekryteringsexpertis som
          moderbolaget. I förberedande syfte går våra utbildare en intern
          utbildning om yrkeshögskolans struktur samt vägleds av en forskare
          inom pedagogik. Därmed ser vi till att undervisningen är relevant för
          era elever och tar ansvar för utbildningens röda tråd.
        </p>
      </section>
      <section class="offer">
        <h2>Det här erbjuder vi</h2>

        <ul>
          <li>
            <p>Utbildning inom IT</p>
          </li>
          <li>
            <p>Deltagande i ledningsgrupper</p>
          </li>
          <li>
            <p>Kodstugor</p>
          </li>
          <li>
            <p>Hela utbildningspaket eller enstaka kurser</p>
          </li>
          <li>
            <p>Gästföreläsningar</p>
          </li>
          <li>
            <p>Framtagning av kursmaterial och kursplaner</p>
          </li>
        </ul>
      </section>
      <section class="contact">
        <h2>kontakta oss</h2>
        <p>
          Hör av dig direkt till någon av våra medarbetare. <br />
          Vi återkommer så fort vi kan.
        </p>
        <div class="cards">
          <contact-cards
            v-for="contact in contactPersons"
            :key="contact.name"
            :fullName="contact.fullName"
            :email="contact.email"
            :number="contact.number"
            :title="contact.title"
          />
        </div>

        <div class="teachers-container">
          <h2>våra utbildare</h2>

          <div class="container">
            <teacher-card
              v-for="teacher in teachers"
              :key="teacher.fullName"
              :fullName="teacher.fullName"
              :title="teacher.title"
              :skills="teacher.skills"
            />
          </div>
        </div>

        <div class="lia-container">
          <h2>våra LIA praktikanter</h2>

          <div class="container">
            <lia-card
              v-for="student in liaStudents"
              :key="student.fullname"
              :fullName="student.fullName"
              :title="student.title"
              :desc="student.desc"
            />
          </div>
        </div>
      </section>
      <section class="collab">
        <h2>våra sammarbeten</h2>
        <p>
          Sedan starten 2020 samarbetar vi med flera yrkeshögskolor och företag
          i Göteborg. För oss är det viktigt att vår undervisning överensstämmer
          med elevernas behov och målsättningar och arbetar därför arbetar vi
          nära våra samarbetspartners för att nå fram till en passande plan. Vår
          vision är att erbjuda den mest aktuella kunskapen inom IT och
          programmering på bästa pedagogiska vis.
        </p>

        <div class="collabs">
          <article>
            <img src="../assets/images/logos/codic.png" alt="" />
            <p>CODIC</p>
          </article>
          <article>
            <img src="../assets/images/logos/campusMölndal.jpg" alt="" />
            <p>campus mölndal</p>
          </article>
          <article>
            <img src="../assets/images/logos/ECutbildning.jpg" alt="" />
            <p>EC utbildning</p>
          </article>
          <article>
            <img src="../assets/images/logos/FS.png" alt="" />
            <p>future skill</p>
          </article>
          <article>
            <img src="../assets/images/logos/Handelsakademin.png" alt="" />
            <p>Handelsakademin</p>
          </article>
          <article>
            <img src="../assets/images/logos/myh.png" alt="" />
            <p>Myndigheten för yrkeshögskolan</p>
          </article>
          <article>
            <img src="../assets/images/logos/newton.png" alt="" />
            <p>newton</p>
          </article>
          <article>
            <img src="../assets/images/logos/jensen-education.svg" alt="" />
            <p>jensen education</p>
          </article>
        </div>
      </section>
      <section class="reviews">
        <h2>Vad tycker eleverna?</h2>
        <p>
          Våra IT-lärare arbetar för att förmedla komplexa ämnen på ett så
          pedagogiskt, engagerande och tydligt sätt som möjligt. På
          YH-utbildningar runtom i Göteborg har de blivit uppskattade av både
          utbildningsledare och elever för väl utförda och strukturerade kurser
          och utbildningar. Här nedan kan du läsa den respons som våra IT-lärare
          har mottagit från sina elever.
        </p>
        <div class="rev-section">
          <review-cards
            v-for="review in reviews"
            :key="review.review"
            :review="review.review"
            :reviewer="review.reviewer"
          />
        </div>
      </section>
    </main>

    <Footer />
  </div>
</template>

<script>
import DiskNav from "../components/Navigation/DiskNavbar.vue"
import MobileNavbar from "../components/Navigation/MobileNavbar.vue"

import ContactCards from "../components/ContactCards.vue"
import ReviewCards from "../components/ReviewCards.vue"
import TeacherCard from "../components/TeacherCard.vue"
import LiaCard from "../components/LiaCard.vue"

import Footer from "../components/Footer/Footer.vue"
export default {
  components: {
    DiskNav,
    MobileNavbar,
    ContactCards,
    TeacherCard,
    LiaCard,
    ReviewCards,
    Footer,
  },
  computed: {
    contactPersons() {
      return this.$store.state.contactPersons
    },
    reviews() {
      return this.$store.state.reviews
    },
    teachers() {
      return this.$store.state.teachers
    },
    liaStudents() {
      return this.$store.state.liaStudents
    },
  },
  created() {
    window.scrollTo(0, 0)
    this.$store.dispatch("getTeachers")
    this.$store.dispatch("getStudents")
    this.$store.dispatch("getReviews")
  },
}
</script>

<style lang="scss" scoped>
@import "../assets/styles/globalStyles.scss";
.about {
  @include flex();
  width: 100vw;
  min-height: 100vh;

  h2 {
    color: $main-color;
    text-transform: uppercase;
    margin: 1.5rem 0rem;
  }

  p {
    color: #aaa;
    line-height: 1.8rem;
  }
  main {
    @include flex();
    align-items: flex-start;
    min-height: 100vh;
    width: 100vw;

    .head {
      @include flex();
      width: 100%;
      min-height: 80vh;
      background: url("../assets/images/bg.jpg");
      background-size: cover;
      background-repeat: no-repeat;
      background-attachment: fixed;

      blockquote {
        font-size: 2.4rem;
        font-weight: bold;
        font-family: "Montserrat", sans-serif;
        text-transform: uppercase;
        color: $main-color;
      }

      p {
        margin: 2rem;
        max-width: 40rem;
        line-height: 2rem;
        color: #f2f2f2;
      }
    }

    .about-us {
      width: 100%;
      padding: 10rem 3rem;
      @include flex();

      p {
        max-width: 50rem;
        span {
          color: #efefef;
          font-weight: bold;
        }
      }
    }

    .offer {
      width: 100%;
      padding: 4rem;
      @include flex();
      align-items: flex-start;
      background: #ffffff06;

      ul {
        @include flex();
        //justify-content: flex-start;
        flex-direction: row;
        flex-wrap: wrap;

        li {
          width: 30%;
          flex-grow: 4;
          margin: 1rem;
          text-align: left;
        }
      }
    }

    .contact {
      width: 100%;
      min-height: 80vh;
      @include flex();
      padding: 10rem 0rem 6rem 0rem;

      .cards {
        width: 100%;
        margin: 4rem 0rem;
        @include flex();
        flex-direction: row;
        flex-wrap: wrap;
      }

      .teachers-container {
        width: 100%;
        padding: 1rem 4rem;
        .container {
          @include flex();
          flex-direction: row;
          flex-wrap: wrap;
        }
      }

      .lia-container {
        width: 100%;
        padding: 1rem 4rem;
        margin-top: 4rem;
        .container {
          padding: 2rem 1rem;

          @include flex();
          justify-content: flex-start;
          flex-direction: row;
          flex-wrap: wrap;
        }
      }
    }

    .collab {
      width: 100%;
      @include flex();
      align-items: flex-start;
      min-height: 40vh;
      text-align: left;
      //background: #efefef;

      h2 {
        padding: 0rem 4rem;
      }
      p {
        max-width: 65rem;
        padding: 0rem 4rem;
      }

      .collabs {
        margin: 4rem 0rem;
        padding: 2rem 6rem;
        width: 100%;
        @include flex();
        flex-direction: row;
        flex-wrap: wrap;
        justify-content: center;
        align-items: flex-end;
        background: #fdfdfd;

        article {
          margin: 2rem 4rem;
          @include flex();
          justify-content: space-between;

          p {
            color: #888;
            margin: 2rem 0rem;
            //font-weight: bold;
            font-size: 0.9rem;
            text-transform: capitalize;
            padding: 0rem;
          }

          img {
            height: 6rem;
          }
        }
      }
    }

    .reviews {
      width: 100%;
      @include flex();
      align-items: flex-start;
      padding: 4rem;
      text-align: left;

      p {
        max-width: 65rem;
      }

      .rev-section {
        margin: 4rem 0rem;
        width: 100%;
        @include flex();
        flex-direction: row;
        flex-wrap: wrap;
      }
    }
  }
}

@media only screen and (max-width: 768px) {
  .about {
    main {
      p {
        font-size: 0.9rem;
        text-align: left;
      }

      h2 {
        font-size: 1.3rem;
      }

      .head {
        background: url("../assets/images/bg-mobile.jpg");
        background-size: cover;
        background-repeat: no-repeat;

        blockquote {
          font-size: 1.7rem;
        }
      }

      .about-us {
        padding: 8rem 2rem;
      }

      .offer {
        padding: 4rem 2rem;
        ul {
          width: 100%;
          flex-direction: column;
          margin: 2rem 0rem;
          padding: 0rem 1.5rem;

          li {
            width: 100%;
            flex-grow: initial;
            margin: 0.6rem 0rem;

            p {
              line-height: 1.4rem;
            }
          }
        }
      }

      .contact {
        p {
          text-align: center;
          margin: 0rem 2rem;
          font-size: 0.8rem;
          line-height: 1.4rem;
        }

        .teachers-container {
          padding: 1rem;
        }
        .lia-container {
          padding: 1rem;
        }
      }

      .collab {
        h2 {
          padding: 0rem 2rem;
        }
        p {
          padding: 0rem 2rem;
        }

        .collabs {
          padding: 1rem;
          article {
            margin: 1rem 0.6rem;

            p {
              font-size: 0.8rem;
            }

            img {
              height: 4rem;
            }
          }
        }
      }

      .reviews {
        padding: 4rem 2rem;

        h2 {
          //font-size: 1rem;
        }
      }
    }
  }
}
</style>
