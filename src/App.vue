<script>
import axios from 'axios'
export default {
	name: 'App',
	data() {
		return {
			posts: [],
			users: [],
			photos: []
		}
	},
	mounted() {
		this.getPosts()
		this.getUsers()
		this.getPhotos()
	},
	methods: {
		getPosts() {
		axios.get('https://jsonplaceholder.typicode.com/posts')
			.then((response) => {
				console.log(response.data)
				this.posts = response.data
			})
			.catch((error) => {
				console.log(error)
			})
		},
		getUsers() {
		axios.get('https://jsonplaceholder.typicode.com/users')
			.then((response) => {
				console.log(response.data)
				this.users = response.data
			})
			.catch((error) => {
				console.log(error)
			})
		},
		getUsername(userId) {
      const user = this.users.find(user => user.id === userId)
      if (user) {
        return user.username
      }
      return 'Unknown user'
    },
		getPhotos() {
		axios.get('https://jsonplaceholder.typicode.com/photos')
			.then((response) => {
				console.log(response.data)
				this.photos = response.data
			})
			.catch((error) => {
				console.log(error)
			})
		},
		getImage(userId) {
			const photo = this.photos.find(photo => photo.id === userId)
			if (photo) {
				return photo.url
			}
			return 'Unknown image'
		}
	}
}
</script>

<template>
	<header class="header">
		<div class="container">
			<div class="nav">
				<div class="nav__logo">
					<img src="./assets/img/logoImage.svg" alt="logo">
				</div>
				<div class="nav__item">
					<a href="#">my_profile</a>
				</div>
			</div>
			<hr>
		</div>
	</header>
	<section class="chat">
		<div class="container">
			<div v-for="post in posts" :key="post.id">
				<div class="post">
				<div class="post__description">
					<img class="description__img" :src="getImage(post.userId)" alt="user-logo">
				</div>
				<div class="post__main">
					<div class="main__user">
						<div class="user__indicator">
							<img src="./assets/img/active.png" alt="active-indicator">
						</div>
						<p class="user__name">{{ getUsername(post.userId) }}</p>
						<button class="user__edit">...</button>
					</div>
					<div class="main__text">
						<p>{{ post.body }}</p>
					</div>
				</div>
			</div>
			<hr>
			</div>
		</div>
	</section>
</template>

<style>
</style>
