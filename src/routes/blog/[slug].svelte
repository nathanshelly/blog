<script context="module" lang="ts">
  import type {Preload} from '@sapper/common'

  export const preload: Preload = async function (this, {params: {slug}}) {
    // the `slug` parameter is available because
    // this file is called [slug].html
    const res = await this.fetch(`blog/${slug}.json`)
    const data = await res.json()

    if (res.status === 200) {
      return {post: data}
    } else {
      this.error(res.status, data.message)
    }
  }
</script>

<script lang="ts">
  import type {Post} from './_posts'

  export let post: Post
</script>

<style>
  header {
    text-align: center;
  }

  header h1 {
    margin-bottom: 0.7em;
  }

  header p {
    color: #aaa;
    text-transform: uppercase;
    font-family: Rubik, sans-serif;
    font-weight: 600;
  }

  header hr {
    min-width: 100px;
    width: 30%;
  }
</style>

<svelte:head>
  <title>{post.title}</title>
</svelte:head>

<header>
  <p>{post.printDate} ~ {post.printReadingTime}</p>
  <h1>{post.title}</h1>
  <hr />
</header>
<div class="container">
  <article class="content">
    {@html post.html}
  </article>
  <hr />
</div>
