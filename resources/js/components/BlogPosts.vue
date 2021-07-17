<template>
    <div class="blog-section">
        <div class="container">
            <h1 class="text-center">From Our Blog</h1>

            <p class="section-description">We turn ideas into great digital products with strong focus in building long term relationships with our clients. Our main expertise is developing native mobile apps and web projects regardless of which industry you are in, but we do have deep experience in working with companies in Health, Media, DIgital Publishers and AdTech in general.</p>

            <div class="blog-posts">
                <div v-for="post in posts" :key="post.id" class="blog-post">
                    <a :href="post.link">
                        <blog-image
                            :url="post._links['wp:featuredmedia'][0].href">
                        </blog-image>
                    </a>
                    <a :href="post.link"><h2 class="blog-title">{{ post.title.rendered }}</h2></a>
                    <div class="blog-description">{{ stripTags(post.excerpt.rendered) }}</div>
                </div>
            </div>
        </div> <!-- end container -->
    </div> <!-- end blog-section -->
</template>

<script>
import BlogImage from './BlogImage'
import sanitizeHtml from 'sanitize-html'

export default {
    components: {
        BlogImage,
    },
    created() {
        axios.get('https://blog.laravelecommerceexample.ca/wp-json/wp/v2/posts?per_page=3')
            .then(response => {
                this.posts = response.data
            })
    },
    data() {
        return {
            posts: []
        }
    },
    methods: {
        stripTags(html) {
            return sanitizeHtml(html, {
                allowedTags: []
            }).substring(0, html.indexOf('&hellip;'))
        }
    }

}
</script>

