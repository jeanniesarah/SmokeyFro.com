<template>
	<Layout :sidebar="true" :top="false" :bottom="true">
		<article>
			<h1 class="title">{{ $page.post.title }}</h1>
			<p class="lead" v-html="$page.post.excerpt" />
            <div class="grid w-full grid-cols-1 gap-4 mt-6 mb-6 album-grid md:mb-20 md:mt-10 sm:grid-cols-2 lg:grid-cols-4" :class="$page.post.albumClass">
                <a v-for="(photo, $index) in $page.post.photos" :key="$index" :href="photo.full.src" data-fslightbox="gallery" class="block overflow-hidden transition-all duration-300 ease-in-out border border-white border-solid rounded-md shadow-sm opacity-100 hover:opacity-75 hover:border-accent hover:shadow-lg image">
                    <g-image :src="photo.thumb.src" width="250" class="object-cover w-full rounded-md" />
                </a>
            </div>
			<RelatedAlbums :id="$page.post.id" :category="$page.post.category.title" />
			<p><a @click.prevent="$router.go(-1)" href="#" class="mr-3 font-bold">&larr; Back</a></p>
		</article>
		<template slot="navgroup">
			About
		</template>
		<template slot="secondary-nav">
			<NavAbout />
		</template>
		<template slot="repo_link">
			<a href="https://github.com/smokeyfro/smokeyfro/blob/master/src/templates/Album.vue">Source</a>
		</template>
	</Layout>
</template>

<script>
import NavAbout from "@/components/NavAbout";
import RelatedAlbums from "@/components/RelatedAlbums";
import { sampleSize } from "lodash";

export default {
	components: {
		NavAbout,
		RelatedAlbums
	},
    data() {
		return {
			toggler: false,
			options : {
				closeText : 'X'
			}
		}
	},
	metaInfo() {
		return {
			title: `${this.$page.post.title}`,
			bodyAttrs: {
				class: "about photos single"
			},
			script: [
				{ src: "/fslightbox.js", defer: true, type: "text/javascript" },
			]
		};
	},
	computed: {
		config() {
			return config;
		}
    }
};
</script>

<page-query>
	query Album($path: String){
		post: album(path: $path) {
			title
			slug
			id
			excerpt
			content
			albumClass
			category {
				title
			}
			photos {
				full
				thumb
			}
			path
		}
	}
</page-query>
<style>
@media ( min-width: 1024px ) {
	.grid-style1 {
		& > a:first-of-type,
		& > a:nth-of-type(7),
		& > a:nth-of-type(13) {
			grid-column: span 2;
			grid-row: span 2;
		}
	};

	main .grid-style2 > a:nth-of-type(3),
	main .grid-style2 > a:nth-of-type(6),
	main .grid-style2 > a:nth-of-type(13) {
	grid-column: span 2;
	grid-row: span 2;
	}

	main .grid-style3 > a:nth-of-type(2),
	main .grid-style3 > a:nth-of-type(5),
	main .grid-style3 > a:nth-of-type(10) {
	grid-column: span 3;
	grid-row: span 3;
	}

	main .grid-style1 > a:first-of-type img,
	main .grid-style1 > a:nth-of-type(7) img,
	main .grid-style1 > a:nth-of-type(13) img,
	main .grid-style2 > a:nth-of-type(3) img,
	main .grid-style2 > a:nth-of-type(6) img,
	main .grid-style2 > a:nth-of-type(13) img,
	main .grid-style3 > a:nth-of-type(2) img,
	main .grid-style3 > a:nth-of-type(5) img,
	main .grid-style3 > a:nth-of-type(10) img {
		height: 110%;
	}
}

@media ( min-width: 1024px ) {
	.grid-style1 {
		& > a:first-of-type,
		& > a:nth-of-type(7),
		& > a:nth-of-type(13) {
			grid-column: span 2;
			grid-row: span 2;
		}
	};

	main .grid-style2 > a:nth-of-type(3),
	main .grid-style2 > a:nth-of-type(6),
	main .grid-style2 > a:nth-of-type(13) {
	grid-column: span 2;
	grid-row: span 2;
	}

	main .grid-style3 > a:nth-of-type(2),
	main .grid-style3 > a:nth-of-type(5),
	main .grid-style3 > a:nth-of-type(10) {
	grid-column: span 3;
	grid-row: span 3;
	}

	main .grid-style1 > a:first-of-type img,
	main .grid-style1 > a:nth-of-type(7) img,
	main .grid-style1 > a:nth-of-type(13) img,
	main .grid-style2 > a:nth-of-type(3) img,
	main .grid-style2 > a:nth-of-type(6) img,
	main .grid-style2 > a:nth-of-type(13) img,
	main .grid-style3 > a:nth-of-type(2) img,
	main .grid-style3 > a:nth-of-type(5) img,
	main .grid-style3 > a:nth-of-type(10) img {
		height: 110%;
	}
}

</style>