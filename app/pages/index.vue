<template>
  <section class="home">
    <div class="py-24 md:py-36 mx-auto flex flex-wrap flex-col md:flex-row items-center">
      <div class="flex flex-col w-full xl:w-3/5 justify-center lg:items-start overflow-y-hidden">
        <div  class="home__welcome text-4" >
          Welcome to KZPporkChef, this is not only a cooking application, but also your best assistant for grilling pork chops. In the unique world of taste, we take you to explore the mystery of delicious food.

KZPporkChef is unusual because it is not just a simple list of recipes, but a true master of pork. Here, you are the director of cooking, and our app is your right-hand assistant, allowing you to master every pork chop with ease.

Choose your favorite type of pork, from tender pork tenderloin to juicy pork chops, we've got you covered to satisfy your discerning taste buds. When it comes to doneness, KZPporkChef doesn’t just mean “cooked”. We understand that every doneness is a taste adventure.

What's unique is that we don't just tell you how long you should cook it for, we more precisely calculate the most appropriate internal temperature. Because every pork chop deserves care, and every cooking session is a profound dialogue with flavor.

KZPporkChef is your secret weapon to challenge the ultimate in cooking and your intimate partner in mastering the art of cooking pork chops. Unleash your creativity, break with tradition and become a master of pork chop cooking!
        </div>

        <div class="mb-12 xl:mb-0">
          <br>
          <br>
          <h2 class="text-6">Email: huynhtrannhu864@gmail.com</h2>

          
        </div>
      </div>
      <div class="flex flex-col w-full xl:w-2/5">
        <img
          alt="Hero"
          class="rounded shadow-xl"
          src="https://source.unsplash.com/random/720x400"
        />
      </div>
    </div>
  </section>
</template>

<script lang="ts">
import { Component, Vue } from 'nuxt-property-decorator';
import settings from '@/content/settings/general.json';

@Component({
  // Called to know which transition to apply
  transition() {
    return 'slide-left';
  },
})
export default class Home extends Vue {
  welcomeText = settings.welcomeText;

  get posts(): Post[] {
    return this.$store.state.posts;
  }

  isSignedUp = false;

  form = {
    email: '',
  };

  encode(data): string {
    return Object.keys(data)
      .map((key) => `${encodeURIComponent(key)}=${encodeURIComponent(data[key])}`)
      .join('&');
  }

  validEmail(email): boolean {
    // eslint-disable-next-line
    const re = /^(([^<>()\[\]\\.,;:\s@"]+(\.[^<>()\[\]\\.,;:\s@"]+)*)|(".+"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,}))$/;
    return re.test(email);
  }

  async handleSubmit(): Promise<void> {
    if (!this.validEmail(this.form.email)) {
      this.$refs.emailInput.focus();
      return;
    }

    try {
      await fetch('/', {
        method: 'POST',
        headers: { 'Content-Type': 'application/x-www-form-urlencoded' },
        body: this.encode({ 'form-name': 'signups', ...this.form }),
      });

      this.isSignedUp = true;
    } catch (error) {
      console.error(error);
    }
  }
}
</script>
