<template>
  <div class="bg-white dark:bg-slate-800">
    <div>
      <Nav />
      <div class="pt-16 sm:pt-32">
        <div class="relative isolate pt-14 lg:px-8">
          <PatchesLarger />
          <div
            class="mx-auto lg:max-w-7xl lg:flex justify-center max-w-lg px-8 sm:px-0"
          >
            <div class="text-left sm:pb-8 max-w-xl">
              <h1
                class="text-4xl font-bold tracking-tight text-gray-900 sm:text-6xl dark:text-white"
              >
                June Conference
              </h1>
              <h2
                class="text-3xl mt-6 font-semibold tracking-tight text-gray-900 dark:text-white"
              >
                Key Details
              </h2>
              <p
                class="mt-3 text-lg leading-8 text-gray-600 dark:text-slate-300"
              >
                Dates: 29 and 30 May, 5 June <br />
                Venue: NUS School of Computing
              </p>

              <p
                class="mt-3 text-lg leading-8 text-gray-600 dark:text-slate-300"
              >
                The June Conference is our flagship computing event held at NUS
                School of Computing. This year, the theme is
                <b>Artificial Intelligence</b>. We are holding over 17
                workshops, 5 talks and 3 hackathons over 3 tracks to cater to
                various skill levels!
              </p>

              <div class="mt-6">
                <Disclosure
                  v-for="(faq, index) in faqs"
                  :key="index"
                  v-slot="{ open }"
                >
                  <DisclosureButton
                    class="mt-2 flex items-center justify-between rounded-lg bg-orange-100 px-4 py-2 text-left sm:text-xl text-orange-900 hover:bg-orange-200 focus:outline-none focus-visible:ring focus-visible:ring-orange-500 focus-visible:ring-opacity-75 text-md font-semibold tracking-tight w-full"
                  >
                    <span>{{ faq.question }}</span>
                    <ChevronUpIcon
                      :class="open ? 'rotate-180 transform' : ''"
                      class="h-5 w-5 text-orange-500"
                    />
                  </DisclosureButton>
                  <DisclosurePanel
                    class="px-4 py-4 pb-2 text-lg text-gray-600 dark:text-slate-300"
                  >
                    <span v-html="faq.answer"></span>
                  </DisclosurePanel>
                </Disclosure>
              </div>

              <div class="text-left pb-4 sm:pb-12 max-w-xl mt-12">
                <h2
                  class="text-3xl mt-6 font-semibold tracking-tight text-gray-900 dark:text-white"
                >
                  Find out how the BBCS Hackathon turned out.
                </h2>
                <div class="mt-8">
                  <NuxtLink
                    href="https://buildingblocs-2023.devpost.com/project-gallery"
                    class="rounded-md bg-orange-500 px-3.5 py-3.5 text-medium font-semibold text-white shadow-sm hover:bg-orange-600 focus-visible:outline focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-orange-500"
                  >
                    See Project Gallery
                    <span aria-hidden="true">&rarr;</span>
                  </NuxtLink>
                </div>
              </div>

              <h2
                class="text-3xl mt-3 font-semibold tracking-tight text-gray-900 dark:text-white mb-8"
              >
                Photo Gallery
              </h2>
              <div class="">
                <Swiper
                  :modules="[
                    SwiperAutoplay,
                    SwiperPagination,
                    SwiperNavigation,
                  ]"
                    :pagination="{
                      clickable: true,
                    }"
                  :navigation="true"
                  :centeredSlides="true"
                  :autoplay="{ delay: 3000, disableOnInteraction: false }"
                  class="h-96 rounded-2xl mb-4"
                >
                  <SwiperSlide v-for="slide in images" :key="slide">
                    <nuxt-img
                      format="webp"
                      class="object-cover h-96 w-full absolute top-0"
                      :src="slide"
                    />
                  </SwiperSlide>
                </Swiper>
              </div>
            </div>
            <div class="mx-1 md:mx-7">
              <div class="mx-1 md:mx-7 max-w-lg">
                <div class="mx-1 md:mx-7 max-w-lg">
                  <p class="text-sm sm:text-md leading-5 font-bold text-gray-300 dark:text-gray-600">
                      Official Poster
                  </p>
                  <!-- <div> -->
                    <Swiper
                      :modules="[
                        SwiperAutoplay,
                        SwiperPagination,
                        SwiperNavigation,
                      ]"
                        :pagination="{
                          clickable: true,
                        }"
                      :navigation="true"
                      :centeredSlides="true"
                      :autoplay="{ delay: 3000, disableOnInteraction: false }"
                      class="rounded-xl h-[40rem]"
                    >
                      <SwiperSlide v-for="poster in posters" :key="poster">
                        <nuxt-img
                          format="webp"
                          class="object-cover object-center w-full h-[40rem] absolute top-0"
                          :src="poster"
                        />
                      </SwiperSlide>
                    </Swiper>
                  <!-- </div> -->

                  <h2 class="text-3xl font-bold mt-12 mb-4 text-gray-900 sm:text-4xl dark:text-white">
                    Tracks
                  </h2>

                  <TabGroup :defaultIndex="0">
                    <TabList
                      class="flex item-center justify-center mx-auto mb-4 mt-8"
                    >
                      <Tab
                        v-for="(category, index) in tracks.map(
                          (it) => it.trackTitle,
                        )"
                        as="template"
                        :key="category"
                        v-slot="{ selected }"
                      >
                        <button
                          :class="[
                            'w-full text-medium leading-5 font-bold',
                            'focus:outline-none justify-center',
                            selected
                              ? 'text-orange-700 dark:text-orange-300'
                              : 'text-orange-600 dark:text-orange-100 text-opacity-40 hover:text-orange-300 hover:text-opacity-70',
                          ]"
                        >
                          {{ category }}
                        </button>
                      </Tab>
                    </TabList>
                    <TabPanels>
                      <TabPanel
                        v-for="(timelines, index) in tracks"
                        :key="index"
                        v-slot="{ selected }"
                        class="p-3 focus:outline-none"
                      >
                        <div
                          v-for="timeline in timelines.timeline"
                          :key="timeline.date"
                        >
                          <h3
                            class="text-2xl font-semibold tracking-tight text-gray-900 sm:text-3xl dark:text-white mb-4"
                          >
                            {{ timeline.date }}
                          </h3>
                          <ol
                            class="relative border-l border-gray-200 dark:border-gray-700 mb-10"
                          >
                            <li
                              v-for="event in timeline.events"
                              :key="event.title"
                              class="mb-10 ml-4"
                            >
                              <div
                                class="absolute w-3 h-3 bg-gray-200 rounded-full mt-1.5 -left-1.5 border border-white dark:border-gray-800 dark:bg-gray-600"
                              ></div>
                              <h3
                                class="text-lg font-semibold tracking-tight text-gray-900 sm:text-xl dark:text-white"
                              >
                                {{ event.title }}
                              </h3>
                              <div class="flex items-center">
                                <p
                                  class="sm:text-md text-md grow text-gray-500 dark:text-slate-400"
                                >
                                  <i>{{ event.author }}</i>
                                </p>
                                <NuxtLink v-if="event.youtube"
                                  :href="event.youtube"
                                  class="text-gray-500 hover:text-gray-900 dark:hover:text-white mx-4"
                                >
                                  <IconsYoutube />
                                </NuxtLink>

                              </div>
                              

                              <nuxt-img
                                format="webp"
                                v-if="event.image"
                                :src="event.image"
                                alt=""
                                class="object-cover object-center w-full max-h-[25rem] lg:max-h-full rounded-xl shadow-xl ring-1 ring-gray-400/10 my-2"
                              />
                            </li>
                          </ol>
                        </div>
                      </TabPanel>
                    </TabPanels>
                  </TabGroup>
                </div>
              </div>
            </div>
          </div>
          <EventsCta />
          <Footer />
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import {
  Disclosure,
  DisclosureButton,
  DisclosurePanel,
  TabGroup,
  TabList,
  Tab,
  TabPanels,
  TabPanel,
} from "@headlessui/vue";
import { ChevronUpIcon } from "@heroicons/vue/20/solid";

const images = [
  "/june/img1.png",
  "/june/img2.jpg",
  "/june/img3.jpg",
  "/june/img4.png",
  "/june/dataproc.png",
  "/june/openai.jpg",
  "/june/dl.jpg",
  "/june/figma.png",
  "/june/flask1.jpg",
  "/june/gnns.jpg",
  "/june/intai.jpg",
  "/june/introai.jpg",
  "/june/opencv.png",
  "/june/python.jpg",
];

const posters = [
  1,2,3,4
].map(it => `/june/poster/${it}.png`)

function link(text, url) {
  return `<a href="${url}" class="text-orange-500 dark:text-orange-400 hover:underline">${text}</a>`;
}

const faqs = [
  {
    question: "Must I be present the entire time for the June Conference?",
    answer:
      "You may be excused for one day of the conference if you have other commitments / events, although you are encouraged to come on all days since the workshops progressively build on your knowledge!",
  },
  {
    question: "Is there an online rendition of the conference?",
    answer:
      "We seek for optimal engagement during this year’s conference and therefore it will be fully physical, not online.",
  },
  {
    question: "Why should I sign up?",
    answer: "You can learn a whole lot of new skills and it’ll be really fun!",
  },
  {
    question: "How will I receive my prizes?",
    answer:
      "The prize giving ceremony will be conducted on-site on Day 3, 5th June.",
  },
  {
    question: "What are the prizes?",
    answer:
      "We cannot reveal anything at this point, but we are coordinating a large pool of prizes with our sponsor, Meta! All we can guarantee is that a large number of people will walk away with amazing prizes!",
  },
  {
    question: "Must I go for all workshops / talks?",
    answer:
      "Yes, all tracks require certain skills which will be taught progressively in the workshops!",
  },
  {
    question: "What if something pops up and I can’t make it?",
    answer: `
        Email us at ${link(
          "hello@buildingblocs.sg",
          "mailto:hello@buildingblocs.sg",
        )}
        or approach us on ${link("Discord", "https://discord.gg/VSHyrbsJFs")} 
        in any appropriate channels and we will update your signup status accordingly.
        `,
  },
  {
    question: "How will the hackathon group be allocated?",
    answer:
      "We will be allocating them randomly, but we’ll make sure that there’s at least there’s at least one person from your school!",
  },
  {
    question: "Is the event free?",
    answer: "Yep, thanks to our generous sponsors, it’s completely free!",
  },
];

const tracks = [
  {
    trackTitle: "Beginner",
    timeline: [
      {
        date: "Day 1",
        events: [
          {
            title: "Basic Introduction to AI",
            author: "by Lam Yik Ting (DHS) and James Tan Dejun (RVHS)",
            image: "/june/introai.jpg",
          },
          {
            title: "Intro to Python (Part 1)",
            author: "by Wayne Ang, Edwin Liew, Wabiba and Zhe Kai (ACJC)",
            image: "/june/python.jpg",
          },
          {
            title: "Intro to Design Thinking",
            author: "by Du Yuhan (MGS)",
            image: "/june/figma.png",
          },
        ],
      },
      {
        date: "Day 2",
        events: [
          {
            title: "Insights into OpenAI API",
            author: "by Teh Kim Wee (ASRJC)",
            image: "/june/openai.jpg",
            youtube: "https://www.youtube.com/watch?v=gzW6znCRRP4"
          },
          {
            title: "Intro to Python (Part 2)",
            author: "by Wayne Ang, Edwin Liew, Wabiba and Zhe Kai (ACJC)",
            image: "/june/img2.jpg",
          },
          {
            title: "Introduction to Data Processing",
            author: "by Dhanvine Rameshkumar and Eugene Ang (TJC)",
            image: "/june/img3.jpg",
            youtube: "https://www.youtube.com/watch?v=7fzau5vKwP4"
          },
          {
            title: "Integrating AI with Python",
            author: "by Lam Yik Ting (DHS), Yau Le Qi and Eugene Ang (TJC)",
            image: "/june/intai.jpg",
          },
        ],
      },
    ],
  },
  {
    trackTitle: "Intermediate",
    timeline: [
      {
        date: "Day 1",
        events: [
          {
            title: "Basic Introduction to AI",
            author: "by Lam Yik Ting (DHS) and James Tan Dejun (RVHS)",
            image: "/june/introai.jpg",
          },
          {
            title: "Intro to Data Processing",
            author: "by Khoo Kai Wen (NUSH) and Ma Jinghong (HCI)",
            image: "/june/dataproc.png",
          },
          {
            title: "Intro to Scikit-Learn",
            author:
              "by Karimi Zayan, Khoo Kai Wen (NUSH) and Ma Jinghong (HCI)",
            image: "/june/sklearn.jpg",
          },
        ],
      },
      {
        date: "Day 2",
        events: [
          {
            title: "Insights into OpenAI API",
            author: "by Teh Kim Wee (ASRJC)",
            image: "/june/openai.jpg",
            youtube: "https://www.youtube.com/watch?v=gzW6znCRRP4"
          },
          {
            title: "Intro to Deep Learning",
            author:
              "by Jed Lim (NUSH), Seth Yong (SP) and Ashwin Lokesh (YIJC)",
            image: "/june/dl.jpg",
            youtube: "https://www.youtube.com/watch?v=q2UFVLjRnw4",
          },
          {
            title: "Intro to Computer Vision",
            author: "by Ma Weiyi, Saw Zedong and Harry Cheong (DHS)",
            image: "/june/opencv.png",
          },
        ],
      },
    ],
  },
  {
    trackTitle: "Advanced",
    timeline: [
      {
        date: "Day 1",
        events: [
          {
            title: "Integrating AI into a Flask Application (Part 1)",
            author: "by Yap Yuan Xi and Prannaya Gupta (NUSH)",
            image: "/june/flask1.jpg",
          },
          {
            title: "Transformers and ViTs",
            author: "by Mahir Shah (NUSH) and Ishneet Singh (TJC)",
            image: "/june/img4.png",
          },
        ],
      },
      {
        date: "Day 2",
        events: [
          {
            title: "Insights into OpenAI API",
            author: "by Teh Kim Wee (ASRJC)",
            image: "/june/openai.jpg",
            youtube: "https://www.youtube.com/watch?v=gzW6znCRRP4"
          },
          {
            title: "Graph Neural Networks",
            author: "by Karimi Zayan and Mahir Shah (NUSH)",
            image: "/june/gnns.jpg",
          },
          {
            title: "Introductory MLOps",
            author: "by Mr Guoren Ng (AISG)",
          },
          {
            title: "Integrating AI into a Flask Application (Part 2)",
            author: "by Yap Yuan Xi and Prannaya Gupta (NUSH)",
          },
        ],
      },
    ],
  },
];

useSeoMeta({
  title: "June Conference - BuildingBloCS 2023",
  description: "Ignite your passion in computing",
  ogTitle: "June Conference - BuildingBloCS 2023",
  ogDescription: "Ignite your passion in computing",
  ogImage: "/index/hero/img5.jpg",
  ogUrl: "https://buildingblocs.sg/events/june",
  twitterTitle: "June Conference - BuildingBloCS 2023",
  twitterDescription: "Ignite your passion in computing",
  twitterImage: "/index/hero/img5.jpg",
  twitterCard: "summary_large_image",
});
</script>

<style>
.swiper-button-prev {
  color: #eb9d39;
}

.swiper-button-next {
  color: #eb9d39;
}

.swiper-pagination-bullet-active {
  background-color: #eb9d39;
}
</style>