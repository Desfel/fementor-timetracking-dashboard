<template>
  <div class="page-wrapper">
    <div class="cards-wrapper">
      <div class="main-card">
        <div class="top-part">
          <img src="@/assets/img/image-jeremy.png" alt="Jeremy">

          <div class="top-content">
            <p class="info-text">Report for</p>
            <p class="username">Jeremy Robson</p>
          </div>
        </div>

        <div class="bottom-part">
          <a href="#" class="stat-link" :class="{'is-active' : activeMenu === 'daily'}" @click.prevent="switchMenu('daily')">Daily</a>
          <a href="#" class="stat-link" :class="{'is-active' : activeMenu === 'weekly'}" @click.prevent="switchMenu('weekly')">Weekly</a>
          <a href="#" class="stat-link" :class="{'is-active' : activeMenu === 'monthly'}" @click.prevent="switchMenu('monthly')">Monthly</a>
        </div>
      </div>

      <div class="stat-cards">
        <div class="stat-card" v-for="(cardType, index) in statsArray"  :class="cardType.code + `-card`" v-bind:key="index">
          <div class="card-content">
            <div class="card-header-row">
              <p v-text="cardType.title"></p>

              <svg width="21" height="5" xmlns="http://www.w3.org/2000/svg"><path d="M2.5 0a2.5 2.5 0 1 1 0 5 2.5 2.5 0 0 1 0-5Zm8 0a2.5 2.5 0 1 1 0 5 2.5 2.5 0 0 1 0-5Zm8 0a2.5 2.5 0 1 1 0 5 2.5 2.5 0 0 1 0-5Z" fill="#BBC0FF" fill-rule="evenodd"/></svg>
            </div>
            <div class="card-bottom-row">
              <p class="card-hour" v-text="`${cardType.timeframes[activeMenu].current}hrs`"></p>
              <p class="card-last-hour" v-text="`Previous - ${cardType.timeframes[activeMenu].previous}hrs`">Last week - 36hrs</p>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { mapState } from 'vuex'
import jsonStats from '../json/data.json'

export default {
  data() {
    return {
      statsArray: jsonStats,
      activeMenu: 'daily'
    }
  },
  head() {
    return {
      title: {
        inner: 'Home'
      },
      meta: [
        {
          name: 'description',
          content: `${this.appTitle} home page`,
          id: 'desc'
        }
      ]
    }
  },
  methods: {
    switchMenu(value) {
      this.activeMenu = value
    }
  },
  computed: mapState('app', ['appTitle'])
}
</script>

<style lang="scss" scoped>
@import '@/theme/variables.scss';

.page-wrapper {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;

  .cards-wrapper {
    display: flex;
    padding: 0 5%;
    width: 100%;

    @media (max-width: 1100px) {
      padding: 0 2.5%;
    }

    @media(max-width: 1024px) {
      padding: 60px 40px;
      flex-wrap: wrap;
    }

    @media(max-width: 767px) {
      padding: 60px 24px;
    }
  }

  .main-card {
    display: flex;
    flex-direction: column;
    width: calc((100% - 90px) / 3);
    border-radius: 15px;
    background: $neutralColor2;

    @media (max-width: 1024px) {
      flex-basis: 100%;
      margin-bottom: 24px;
    }

    .top-part {
      padding: 37px 80px 80px 32px;
      background: $primaryColor1;
      border-radius: 15px;

      @media (max-width: 1024px) {
        display: flex;
        align-items: center;
        padding: 35px 39px 34px 35px;
      }

      img {
        width: 78px;
        height: 78px;
        border-radius: 50%;
        filter: drop-shadow(0px 4px 4px rgba(0, 0, 0, 0.25));
        border: 3px solid $white;
      }

      .top-content {
        margin-top: 46px;

        @media (max-width: 1024px) {
          margin: 0 0 0 23px;
        }

        .info-text {
          margin-bottom: 3px;
          font-weight: normal;
          font-size: 15px;
          line-height: 18px;
          color: $neutralColor4;
        }

        .username {
          font-weight: 300;
          font-size: 40px;
          line-height: 47px;
          color: $white;

          @media (max-width: 767px) {
            font-size: 24px;
            line-height: 28px;
          }
        }
      }
    }

    .bottom-part {
      display: flex;
      flex-direction: column;
      padding: 26px 32px;

      @media (max-width: 1024px) {
        flex-direction: row;
      }


      @media (max-width: 767px) {
        justify-content: space-between;
      }

      a {
        font-style: normal;
        font-weight: normal;
        font-size: 18px;
        line-height: 21px;
        color: $neutralColor3;
        transition: color .3s ease-in-out;

        &:hover,
        &.is-active {
          color: $white;
        }

        &:not(:last-child) {
          margin-bottom: 21px;

          @media (max-width: 1024px) {
            margin-bottom: 0;
            margin-right: 21px;
          }

          @media (max-width: 767px) {
            margin: 0;
          }
        }
      }
    }
  }

  .stat-cards {
    display: flex;
    flex-wrap: wrap;
    align-items: stretch;
    margin-left: 30px;
    margin-bottom: -30px;

    @media (max-width: 1024px) {
      width: 100%;
      margin-left: 0;
    }

    @media (max-width: 767px) {
      flex-direction: column;
    }

    .stat-card {
      display: flex;
      flex-direction: column;
      width: calc((100% - 60px) / 3);
      padding-top: 45px;
      border-radius: 15px;
      margin-bottom: 30px;

      @media (min-width: 768px) {
        &:not(:nth-child(3n + 3)) {
          margin-right: 30px;
        }
      }

      @media (max-width: 767px) {
        width: 100%;
      }

      &.work-card {
        background: url('../assets/img/icon-work.svg') top right no-repeat, $workColor;
      }

      &.play-card {
        background: url('../assets/img/icon-play.svg') top right no-repeat, $playColor;
      }

      &.study-card {
        background: url('../assets/img/icon-study.svg') top right no-repeat, $studyColor;
      }

      &.exercise-card {
        background: url('../assets/img/icon-exercise.svg') top right no-repeat, $exerciseColor;
      }

      &.social-card {
        background: url('../assets/img/icon-social.svg') top right no-repeat, $socialColor;
      }

      &.self-care-card {
        background: url('../assets/img/icon-self-care.svg') top right no-repeat, $selfCareColor;
      }

      .card-content {
        display: flex;
        flex-direction: column;
        flex-grow: 1;
        padding: 29px 35px 32px 30px;
        background: $neutralColor2;
        border-radius: 15px 15px 12px 12px;
        color: $white;
        cursor: pointer;
        transition: background-color .3s ease-in-out;

        @media (max-width: 767px) {
          padding: 28px 24px;
        }

        &:hover {
          background-color: hsla(236, 41%, 34%, 1);
        }

        .card-header-row {
          display: flex;
          align-items: center;

          p {
            font-weight: 500;
            font-size: 18px;
            line-height: 21px;
          }

          svg {
            margin-left: auto;
            cursor: pointer;

            &:hover {
              path {
                fill: $white;
              }
            }

            path {
              transition: fill .3s ease-in-out;
            }
          }
        }

        .card-bottom-row {
          margin-top: auto;

          @media (max-width: 767px) {
            display: flex;
            align-items: center;
            margin-top: 6px;
          }

          .card-hour {
            margin-bottom: 8px;
            font-weight: 300;
            font-size: 56px;
            line-height: 66px;

            @media (max-width: 1150px) {
              font-size: 46px;
              line-height: 56px;
            }

            @media(max-width: 767px) {
              font-size: 32px;
              line-height: 38px;
              margin-bottom: 0;
            }
          }

          .card-last-hour {
            font-size: 15px;
            line-height: 18px;
            color: $neutralColor4;

            @media (max-width: 1150px) {
              font-size: 13px;
              line-height: 16px;
            }

            @media(max-width: 767px) {
              margin-left: auto;
            }
          }
        }
      }
    }
  }
}
</style>
