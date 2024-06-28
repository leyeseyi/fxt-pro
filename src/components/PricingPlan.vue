<template>
  <div class="pricing" ref="pricing">
    <div class="pricing-wrap">
      <h2>MEMBERSHIP PLAN</h2>

      <div class="pricing-body" ref="pricing-body">
        <p class="para">Empower your trading journey with Forex Terminators courses. Choose the plan that fits your
          goals and gain access to expert insights and a supportive community.</p>
        <div class="payment-method">
          <div class="circle">
            <p class="inner-circle"></p>
          </div>
          <p class="text">PAY WITH PAYSTACK, DOLLAR CARD/CRYPTO</p>
        </div>
        <div class="price-cards" ref="price-cards">
          <div class="plan" v-for="(plan, index) in pricingPlan" :key="index">
            <span>{{ plan.rating }}</span>
            <h3>{{ plan.plan }}</h3>
            <div class="gradient"></div>
            <h2>{{ plan.price }}</h2>
            <base-button v-if="pricingPlan[index].payOn.length > 0" :title="'Get started'" @click="togglePlanPop(index)"
              class="b-btn z-[10]" />
            <base-button v-if="pricingPlan[index].payOn.length === 0" :title="'Get started'"
              :link="pricingPlan[index].link" class="b-btn z-[10]" />
            <div class="gradient"></div>
            <div class="pros">
              <div class="pro-wrap" v-for="(pro, index) in plan.packages" :key="index">
                <fa-icon :icon="['fas', 'arrow-right']" size="2xs" class="icon" />
                <p>{{ pro }}</p>
              </div>
            </div>
            <img v-lazy="{ src: srcPath }" class="gradient">
            <img src="../assets/icon/middle-gradient.png" alt="gradient"
              class="absolute bottom-10 z-20 opacity-[0.3]" />
          </div>
        </div>
        <div v-if="selectedPlanIndex !== null" class="plan-pop z-50" ref="pop">
          <p><span class="text-[#8C0100]">FXT</span> Terms and Conditions</p>
          <div class="h-[300px] overflow-auto p-5">
            Welcome to Forex Terminators! By accessing or using our website and services, you agree to the following
            terms and conditions. Please read them carefully.
            <p>Membership Eligibility and Application</p>
            To join Forex Terminators, you must be at least 18 years old. Membership may require an application process,
            including a
            dedication test, to ensure that our community is filled with committed and enthusiastic traders. Some areas
            of our community may require a membership fee, which will be clearly outlined during the sign-up process.
            <p>User Responsibilities</p>
            When you register, please provide accurate and complete information and keep it
            updated. You are responsible for maintaining the confidentiality of your account information and for all
            activities that occur under your account. Please comply with all applicable laws and these terms at all
            times.
            <p>Community Rules</p>
            We have a set of community rules designed to ensure a positive and productive
            environment for all members. By joining, you agree to adhere to these rules. Respect, professionalism, and
            constructive feedback are key principles of our community.
            <p>Intellectual Property </p>
            All content provided by Forex Terminators, including educational materials, videos, articles, and other
            resources, is the property
            of the company. You are welcome to use this content for personal, non-commercial purposes, but please do not
            copy, distribute, modify, or create derivative works from our content without our prior written consent.
            <p>Termination of Membership </p>
            You can terminate your membership at any time by notifying us. We reserve the
            right to terminate or suspend your membership if you violate these terms or the community rules, or for any
            other reason at our discretion.
            <p>Disclaimer of Warranties </p>
            Our services are provided "as is" without any warranties, express or implied. We do not guarantee the
            accuracy, completeness, or reliability of any
            content or services provided. Use our services at your own risk.
            <p>Limitation of Liability </p>
            Forex Terminators will not be liable for any indirect, incidental, special, or consequential damages arising
            out of or in
            connection with your use of our services.
            <p>Indemnification </p>
            You agree to indemnify and hold Forex Terminators, its officers, directors, employees, and agents harmless
            from any claims, liabilities, damages, losses, and
            expenses arising from your use of our services or violation of these terms.
            <p>Changes to These Terms</p>
            We may modify these terms at any time. If we make changes, we will notify you via email or through the
            community
            platform. Continued use of our services after such changes constitutes acceptance of the new terms.
            <p>Governing Law </p>
            These terms are governed by the laws of Nigeria. Any disputes arising from these terms will be
            subject to the exclusive jurisdiction of the courts of Nigeria.

          </div>

          <p class="border-t border-t-[#00000065] w-[90%] mx-auto mt-2 "></p>
          <p class="mb-10 mt-2">PayON</p>
          <div class="payOn">
            <div v-for="(option, optionIndex) in pricingPlan[selectedPlanIndex].payOn" :key="optionIndex">
              <label>
                <div class="flex items-start gap-3">
                  <input type="radio" :value="option.name" v-model="selectedPaymentOption"
                    @change="toggleInputFields(option)" />
                  <img :src="option.img" :alt="option.name" class="relative h-[48px]" />
                </div>
                <p class="text-[15px]">{{ option.name }}</p>
              </label>
            </div>
          </div>
          <h6 class="italic my-3">Note: Whop page MAY not load while using your local network IP address. Kindly
            activate your <a class="underline z-30 relative" href='https://protonvpn.com/'>VPN</a> to access
            the whop page.</h6>
          <div class="w-full sm:w-[60%] sm:m-auto flex justify-between">
            <button @click="closetogglePlanPop(selectedPlanIndex)" class="b-btn1 z-50 bg-black">Decline</button>
            <a :href="selectedPaymentLink" class="b-btn1 z-50 bg-[#8C0100] text-center">Accept</a>
          </div>
          <div></div>

        </div>
        <div v-if="selectedPlanIndex !== null" class="hidden lg:absolute bg-[#00000054] w-full h-full z-40"></div>
      </div>
    </div>
    <div v-if="selectedPlanIndex !== null" class="pb-10 mb-5"></div>
  </div>
</template>

<script>
import paystack from '../assets/logo/paystack-logo.png';
import whop from '../assets/logo/Whop-logo.png';

export default {
  name: 'pricingPlan',
  data() {
    return {
      srcPath: require('../assets/icon/plan-gradient.png'),
      pricingPlan: [
        {
          rating: 'MOST DEMANDED',
          plan: 'FXT Free Course',
          price: '$0',
          link: 'https://whop.com/checkout/plan_EJtBNZlfsQp0m?d2c=true',
          packages: [
            'FREE Beginners Guide',
            'Access to FXT Free Signal channel',
            'FXT trading Journal',
            'Lifetime course access',
          ],
          showPlanPop: false,
          payOn: [],
        },
        {
          rating: 'MOST POPULAR',
          plan: 'BASIC MEMBERSHIP',
          price: '$25',
          link: 'https://whop.com/checkout/plan_zd2m8IWnAKVae?d2c=true',
          packages: [
            'FXT VIP Signals',
            'One - Three Trades per week',
            'Trading tutorial course',
            'Live News trading with Ken Jay',
            'Access to FXT community',
            '10% discount on premium membership',
            '1 month subscription',
          ],
          showPlanPop: false,
          payOn: [
            {
              name: "DOLLAR CARD/CRYPTO",
              img: whop,
              link: "https://whop.com/checkout/plan_zd2m8IWnAKVae?d2c=true"
            }
          ]
        },
        {
          rating: 'MORE POPULAR',
          plan: 'PREMIUM MEMBERSHIP',
          price: '$50',
          link: 'https://whop.com/checkout/plan_FtTRe1q9Pc7in?d2c=true',
          packages: [
            'Recorded beginners crash course',
            'One of FXT setup',
            'Weekly Webinars',
            'Access to FXT community',
            '20% discount on Elite membership',
            'Lifetime Mentorship/membership',
            'Fundamental trading method',
          ],
          showPlanPop: false,
          payOn: [
            {
              name: "BANK TRANSFER",
              img: paystack,
              link: "https://paystack.com/pay/FXTBEGINNERSCOURSE"
            },
            {
              name: "DOLLAR CARD/CRYPTO",
              img: whop,
              link: "https://whop.com/checkout/plan_FtTRe1q9Pc7in?d2c=true"
            }
          ]
        },
        {
          rating: 'RECOMMENDED',
          plan: 'ELITE MEMBERSHIP',
          price: '$200',
          link: 'https://whop.com/checkout/plan_Bv0a0lQnVaLlA?d2c=true',
          packages: [
            'Recorded advanced crash courses',
            'All of FXT setup',
            'Live trading with Ken Jay',
            'Access to FXT community',
            'One of FXT Merch',
            'Lifetime Mentorship/membership',
            'Fundamental trading method',
          ],
          showPlanPop: false,
          payOn: [
            {
              name: "BANK TRANSFER",
              img: paystack,
              link: "https://paystack.com/pay/FXTADVANCEDCOURSE"
            },
            {
              name: "DOLLAR CARD/CRYPTO",
              img: whop,
              link: "https://whop.com/checkout/plan_Bv0a0lQnVaLlA?d2c=true"
            }
          ]
        }
      ],
      selectedPlanIndex: null, // Default to no plan selected
      selectedPaymentOption: "", // Default to an empty string
      selectedPaymentLink: "" // Default to an empty string to store the selected link
    };
  },
  methods: {
    scrollToSection(section) {
      const sectionElement = this.$refs[section];
      if (sectionElement) {
        sectionElement.scrollIntoView({ behavior: 'smooth' });
      }
    },
    togglePlanPop(index) {
      this.pricingPlan.forEach((plan, i) => {
        if (i !== index) {
          plan.showPlanPop = false;
        }
      });

      this.pricingPlan[index].showPlanPop = !this.pricingPlan[index].showPlanPop;
      this.selectedPlanIndex = index; // Set the selected plan index

      if (this.pricingPlan[index].payOn.length > 0) {
        // Default to the first payment option if available
        const firstOption = this.pricingPlan[index].payOn[0];
        this.selectedPaymentOption = firstOption.name;
        this.selectedPaymentLink = firstOption.link;
      }

      if (this.pricingPlan[index].showPlanPop) {
        this.$nextTick(() => {
          document.body.style.overflow = 'hidden';
          
          if (window.innerWidth < 800) {
            document.body.addEventListener('wheel', this.preventScroll, { passive: false });
            this.$refs['pricing'].style.height = window.innerHeight + 'px';
            this.scrollToSection('pricing');
          } else {
            this.scrollToSection('pricing-body');
          }
        });
      } else {
        document.body.style.overflow = '';
        document.body.removeEventListener('wheel', this.preventScroll, { passive: false });
      }
    },

    closetogglePlanPop(index) {
      // Update the showPlanPop state for the given index
      this.pricingPlan.forEach((plan, i) => {
        if (i === index) {
          plan.showPlanPop = false;
        }
      });

      // Reset the selected plan index and other properties
      this.selectedPlanIndex = null;
      document.body.style.overflow = '';
      document.body.removeEventListener('wheel', this.preventScroll, { passive: false });
      this.$refs['pricing'].style.height = "auto";
    },

    preventScroll(e) {
      e.preventDefault();
    },

    toggleInputFields(option) {
      this.selectedPaymentLink = option.link; // Set the link for the selected payment option
      this.selectedPaymentOption = option.name; // Set the selected payment option
    }
  }
};
</script>

<style lang="scss" scoped>
.pricing {
  @apply mx-2;

  @screen md {
    @apply mx-4;
  }

  .pricing-wrap {
    @apply flex flex-col w-full gap-8 py-8 justify-center items-center;

    @screen md {
      @apply gap-12 py-12;
    }

    h2 {
      @apply text-xl font-semibold leading-[normal] uppercase;

      @screen md {
        @apply text-2xl;
      }

      @screen lg {
        @apply text-[35px];
      }
    }

    .pricing-body {
      @apply flex flex-col gap-1 justify-center items-center;

      @screen md {
        @apply gap-14
      }

      .para {
        @apply text-center text-base font-normal w-[90%] leading-[22px] mb-2;

        @screen md {
          @apply leading-[30px] text-xl tracking-wide w-4/5;
        }

        @screen lg {
          @apply text-2xl;
        }
      }

      .payment-method {
        @apply flex items-center justify-end gap-2 font-[700] text-2xl;

        @screen md {
          @apply w-[95%]
        }

        .circle {
          @apply w-[18px] h-[18px] bg-[#E6E6E6] rounded-full relative flex justify-center items-center;
        }

        .inner-circle {
          @apply w-[12px] h-[12px] bg-[#8C0100] rounded-full;
        }

        .text {
          @apply text-[14px];
          font-family: 'Goudy Old Style', serif;
        }
      }

      .plan-pop {
        @apply p-8 flex flex-col bg-white text-[#191919] w-full text-left;
        position: fixed;
        top: 0;
        left: 0;
        right: 0;
        bottom: 0;
        align-items: center;
        height: 100vh;
        border-radius: 0;
        overflow-y: auto;

        @screen lg {
          @apply w-1/2 rounded-3xl items-center justify-between;
          position: absolute;
          top: unset;
          left: unset;
          right: unset;
          bottom: unset;
          justify-content: unset;
          align-items: unset;
          height: unset;
        }

        .close-btn {
          @apply absolute top-2 right-2 text-black font-bold text-lg bg-[#AFAFAF] rounded-full w-8 h-8 flex items-center justify-center z-30;
        }

        p {
          @apply text-center font-bold
        }

        .payOn {
          @apply flex justify-center w-full gap-8
        }

        .b-btn1 {
          @apply w-[45%] z-30 px-6 rounded-[44px] text-white text-[25px] relative;

          @screen sm {
            @apply py-2
          }
        }

        .b-btn1:hover::before {
          animation: shine 1.5s ease-out infinite;
        }

        .b-btn1::before {
          content: "";
          position: absolute;
          width: 50px;
          height: 100%;
          background-image: linear-gradient(120deg,
              rgba(255, 255, 255, 0) 30%,
              rgba(255, 255, 255, 0.8),
              rgba(255, 255, 255, 0) 70%);
          top: 0;
          left: -50px;
          opacity: 0.6;
        }

        @keyframes shine {
          0% {
            left: -50px;
          }

          60% {
            left: 100%;
          }

          to {
            left: 100%;
          }
        }
      }

      .price-cards {
        @apply flex flex-col gap-6;

        @screen md {
          @apply flex-row gap-8 flex-wrap justify-center;
        }



        .plan {
          @apply p-8 flex flex-col items-center justify-start gap-5 rounded-3xl bg-[#191919] text-white min-w-[350px] max-w-[400px] relative;
          box-shadow: 8px 9px 25px 2px rgba(0, 0, 0, 0.15);

          @screen md {
            @apply py-16 px-10 gap-10 transition-transform duration-500;

            &:hover {
              @apply translate-y-4 ease-in-out;
            }
          }



          .gradient {
            min-width: inherit;
            max-width: 400px;
            height: 1px;
            background: linear-gradient(to right, gray, transparent 25%, transparent 50%, transparent 75%, gray 100%);
          }

          h3 {
            @apply text-[18px] font-semibold uppercase text-center leading-normal;
            font-family: 'Goudy Old Style';

            @screen md {
              @apply text-[22px];
            }

            @screen lg {
              @apply text-[24px];
            }
          }

          h2 {
            @apply text-4xl font-bold leading-[normal] tracking-wider uppercase;
            font-family: 'Rockwell Nova', 'serif';

            @screen md {
              @apply text-4xl;
            }

            @screen xl {
              @apply text-[43px];
            }
          }



          /* img {
            @apply absolute bottom-0;
          } */

          span {
            @apply text-[12px] bg-[#8C0100] leading-[32.65px] absolute top-0 right-0 px-3 font-normal rounded-s-[14px];

            @screen sm {
              @apply text-[20px] py-1 rounded-tr-3xl
            }
          }

          .b-btn {
            @apply w-full z-30;
          }


          .pros {
            @apply space-y-2 w-full;

            .pro-wrap {
              @apply flex flex-row items-center gap-2;

              @screen md {
                @apply gap-3;
              }

              p {
                @apply text-base text-start font-medium;

                @screen md {
                  @apply text-lg tracking-wider;
                }
              }

              .icon {
                @apply text-black bg-white rounded-full bg-opacity-85 p-2;
              }
            }
          }
        }
      }
    }
  }
}
</style>
