<template>
  <Layout>

    <!-- Page Header-->
    <header
      class="masthead"
      :style="{
        backgroundImage: $page.general.edges[0].node.cover?`url(${GRIDSOME_API_URL + general.cover.url})`:''
      }"
    >
      <div class="container position-relative px-4 px-lg-5">
        <div class="row gx-4 gx-lg-5 justify-content-center">
          <div class="col-md-10 col-lg-8 col-xl-7">
            <div class="site-heading">
              <h1>{{ general.title }}</h1>
              <span class="subheading">{{ general.subtitle }}</span>
            </div>
          </div>
        </div>
      </div>
    </header>
    <!-- Main Content-->
    <div class="container px-4 px-lg-5">
      <div class="row gx-4 gx-lg-5 justify-content-center">
        <div class="col-md-10 col-lg-8 col-xl-7">
          <!-- Post preview-->
          <div v-for="edge in $page.posts.edges" :key="edge.node.id" class="post-preview">
            <g-link :to="'/post/' + edge.node.id">
              <h2 class="post-title">{{ edge.node.title }}</h2>
            </g-link>
            <p class="post-meta">
              <!-- Posted by
              <a href="#!">Start Bootstrap</a> -->
              Posted on {{ edge.node.created_at }}
            </p>
            <p>
              <span v-for="tag in edge.node.tags" :key="tag.id">
                <g-link :to="'/tag/' + tag.id">{{ tag.title }} </g-link>
                &nbsp;&nbsp;
              </span>  
            </p>
            <!-- Divider-->
            <hr class="my-4" />
          </div>
         
          <!-- Pager-->
          <!-- <div class="d-flex justify-content-end mb-4">
            <a class="btn btn-primary text-uppercase" href="#!"
              >Older Posts →</a
            >
          </div> -->
          <pager :info="$page.posts.pageInfo"></pager>
        </div>
      </div>
    </div>
  </Layout>
</template>

<page-query>
  query ($page: Int) {
    posts: allStrapiPost ( perPage: 3, page: $page) @paginate {
      pageInfo {
        totalPages
        currentPage
      }
      edges {
        node {
          id
          title
          created_at
          tags {
            id
            title
          }
        }
      }
    }
    general: allStrapiGeneral {
      edges {
        node {
          id
          title
          subtitle
          cover {
            url
          }
        }
      }
  }
}
</page-query>

<script>
import { Pager } from 'gridsome'  

export default {
  name: 'HomePage',
  metaInfo: {
    title: "Hello, world!",
  },
  components: {
    Pager
  },
  computed: {
    general() {
      return this.$page.general.edges[0].node
    }
  }
};
</script>

<style></style>
