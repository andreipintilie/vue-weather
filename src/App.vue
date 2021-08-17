<template>
	<div id="app">
		<div
			class="app_search text-center d-flex justify-content-center align-items-center"
		>
			<form @submit.prevent="fetchWeather" id="searchForm">
				<input type="text" v-model="city" required autofocus />
				<div class="app_placeholder">Search...</div>
				<i class="fa fa-search" aria-hidden="true"></i>
			</form>
		</div>
		<div
			class="app_weather text-center d-flex justify-content-center align-items-center"
		>
			<div v-if="weather.main && weather.main !== undefined">
				<div class="card mx-auto" style="width: 25rem;">
					<i :class="getWeatherIcon(weather.weather[0].main)"></i>
					<p>{{ weather.weather[0].description }}</p>
					<div class="card-body">
						<p class="card-text h2">
							{{ Math.round(weather.main.temp - 272.15) }}°C
						</p>
						<p class="card-text mt-4">
							{{ weather.name }}, {{ weather.sys.country }}
							<img
								:src="getCountryFlag(weather.sys.country)"
								alt=""
								class="mx-1 mb-1"
							/>
						</p>
						<hr />
						<p class="card-text">
							Feels like: {{ Math.round(weather.main.feels_like - 272.15) }}°C
						</p>
						<p class="card-text mt-2">
							Min temp: {{ Math.round(weather.main.temp_min - 272.15) }}°C
						</p>
						<p class="card-text mt-2">
							Max temp: {{ Math.round(weather.main.temp_max - 272.15) }}°C
						</p>
						<p class="card-text mt-2">
							Pressure: {{ Math.round(weather.main.pressure) }}
						</p>
						<p class="card-text mt-2">
							Humidity: {{ Math.round(weather.main.humidity) }}%
						</p>
					</div>
				</div>
			</div>
			<div v-else class="text-white">
				<h3>Type a city in the search box and press enter!</h3>
			</div>
		</div>
	</div>
</template>

<script>
	import axios from 'axios';

	export default {
		name: 'App',
		data() {
			return {
				city: '',
				api_key: 'd4eb7768eec536b2a8aaeee1b0e094a2',
				weather: {},
			};
		},
		methods: {
			async fetchWeather() {
				if (!this.city) return;
				if (this.city === this.weather.name) return;

				try {
					const response = await axios.get(
						`https://api.openweathermap.org/data/2.5/weather?q=${this.city}&appid=${this.api_key}`
					);
					this.weather = response.data;
				} catch (error) {
					return;
				}
			},
			getCountryFlag(country) {
				return `https://www.countryflags.io/${country}/shiny/24.png`;
			},
			getWeatherIcon(weather_main) {
				let wd = '';

				if (weather_main === 'Clear') {
					wd = 'card-img-top wi wi-day-sunny pt-4 h1';
				} else if (weather_main === 'Clouds') {
					wd = 'card-img-top wi wi-day-cloudy pt-4 h1';
				} else if (weather_main === 'Tornado') {
					wd = 'card-img-top wi wi-tornado pt-4 h1';
				} else if (weather_main === 'Squall') {
					wd = 'card-img-top wi wi-tornado pt-4 h1';
				} else if (weather_main === 'Ash') {
					wd = 'card-img-top wi wi-tornado pt-4 h1';
				} else if (weather_main === 'Dust') {
					wd = 'card-img-top wi wi-tornado pt-4 h1';
				} else if (weather_main === 'Sand') {
					wd = 'card-img-top wi wi-tornado pt-4 h1';
				} else if (weather_main === 'Fog') {
					wd = 'card-img-top wi wi-tornado pt-4 h1';
				} else if (weather_main === 'Haze') {
					wd = 'card-img-top wi wi-tornado pt-4 h1';
				} else if (weather_main === 'Smoke') {
					wd = 'card-img-top wi wi-tornado pt-4 h1';
				} else if (weather_main === 'Mist') {
					wd = 'card-img-top wi wi-tornado pt-4 h1';
				} else if (weather_main === 'Snow') {
					wd = 'card-img-top wi wi-day-snow pt-4 h1';
				} else if (weather_main === 'Rain') {
					wd = 'card-img-top wi wi-day-rain pt-4 h1';
				} else if (weather_main === 'Drizzle') {
					wd = 'card-img-top wi wi-day-sprinkle pt-4 h1';
				} else if (weather_main === 'Thunderstorm') {
					wd = 'card-img-top wi wi-day-snow-thunderstorm pt-4 h1';
				}

				return wd;
			},
		},
	};
</script>

<style lang="scss">
	$app_background: #fff;
	$app_text_color: #f0f0f0;
	$app_accent: #1b72c3;

	@import url('https://fonts.googleapis.com/css2?family=Montserrat&display=swap');
	@import url('https://pro.fontawesome.com/releases/v5.10.0/css/all.css');
	@import url('https://cdnjs.cloudflare.com/ajax/libs/weather-icons/2.0.12/css/weather-icons.min.css');

	* {
		outline: 0;
		margin: 0;
		padding: 0;
		box-sizing: border-box;
	}

	html,
	body {
		overflow-y: hidden;
	}

	#app {
		font-family: 'Montserrat', sans-serif;
		height: 100vh;
		background-color: $app_background;

		.app_search {
			padding-block: 2rem;
		}

		#searchForm {
			position: relative;
			width: 20%;

			input[type='text'] {
				border: 0;
				border-bottom: 1px solid rgba(0, 0, 0, 0.2);
				padding: 0.3rem 0.5rem;
				width: 100%;
				transition: all 0.2s ease-in-out;
			}

			input[type='text']:focus,
			input[type='text']:valid {
				border-bottom: 1px solid $app_accent;
			}

			input[type='text']:focus ~ .fa-search,
			input[type='text']:valid ~ .fa-search {
				border-bottom: 1px solid $app_accent;
				color: $app_accent;
			}

			input[type='text']:focus ~ .app_placeholder,
			input[type='text']:valid ~ .app_placeholder {
				color: $app_accent;
				top: -1.2rem;
				left: 0;
				font-size: 12px;
				font-weight: bold;
			}

			.app_placeholder {
				position: absolute;
				left: 0.8rem;
				display: flex;
				justify-content: center;
				align-items: center;
				top: 0.4rem;
				color: #bebebe;
				user-select: none;
				pointer-events: none;
				transition: all 0.2s ease-in-out;
			}

			.fa-search {
				position: absolute;
				background: white;
				height: 100%;
				display: flex;
				justify-content: center;
				align-items: center;
				top: 0;
				right: 0;
				border-bottom: 1px solid rgba(0, 0, 0, 0.2);
				padding-inline: 0.6rem;
				color: rgba(0, 0, 0, 0.2);
				transition: all 0.2s ease-in-out;
			}
		}

		.app_weather {
			width: 100%;
			height: 100%;

			p {
				user-select: none;
				pointer-events: none;
			}
		}
	}

	@import './scss/_responsivity.scss';
</style>
