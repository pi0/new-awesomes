<template lang="pug">
  div.container.sub-wraper
    div.row
      div.col-md-6.col-sm-12(v-for="sub in subjects")
        div.sub-item
          nuxt-link(:to="'/subject/' + sub.key" v-bind:style="'background-image:url(' + cdn(sub.cover, 'subject', 'subject') + ')'")
            div.detail 
              h2 {{sub.title}}
              article {{sub.sdesc}}

              div.total
                // span 共 {{sub.amount}} 个库
                span 共 43 个库

</template>

<script>
  import axios from '~plugins/axios'
  import _ from 'underscore'
  export default {
    asyncData ({ req, params, query }) {
      return axios().get('subject').then(res => {
        return {
          subjects: _.sortBy(res.data, item => {
            return -item.order
          })
        }
      })
    }
  }
</script>

<style lang="scss" scoped>
  .sub-wraper {
    max-width: 1000px;
    .cover {
      width: 100%
    }
  }

  .sub-item {
    padding: 20px;
    a {
      display: block;
      height: 250px;
      margin: 20px 0;
      border-radius: 2px;
      position: relative;
      background-repeat: no-repeat;
      background-size: cover;
      overflow: hidden;
      background-position: center center;
      position: relative;
      color: #FFF;

      &:after {
        display: block;
        content: '';
        height: 100%;
        background-color: rgba(0, 0, 0, 0.54);
        position: absolute;
        top: 0;
        left: 0;
        width: 100%;
        z-index: 1;
      }

      &:hover {
        &:after {
          background-color: rgba(0, 0, 0, 0.7);
        }
      }

      .detail {
        height: 100%;
        position: absolute;
        top: 0;
        left: 0;
        width: 100%;
        z-index: 10;
        padding: 20px;

        h2 {
          text-align: center;
        }

        article {
          color: rgba(255, 255, 255, 0.9);
          line-height: 30px;
          font-size: 12px;
          height: 60px;
          overflow: hidden;
        }

        .total {
          text-align: center;
          padding-top: 50px;
          span {
            display: inline-block;
            border: #FFF 1px dashed;
            padding: 10px 20px;
          }
        }
      }
    }
  }
</style>
