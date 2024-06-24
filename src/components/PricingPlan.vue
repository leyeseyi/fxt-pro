<template>
  <div class="pricing">
    <div class="pricing-wrap">
      <h2>Pricing Plan</h2>

      <div class="pricing-body">
        <p class="para">Empower your trading journey with Forex Terminators courses. Choose the plan that fits your
          goals and gain access to expert insights and a supportive community.</p>
        <div class="payment-method">
          <div class="circle">
            <p class="inner-circle"></p>
          </div>
          <p class="text">PAY WITH PAYSTACK, DOLLAR CARD/CRYPTO</p>
        </div>
        <div class="price-cards">
          <div class="plan" v-for="(plan, index) in pricingPlan" :key="index">
            <span>{{ plan.rating }}</span>
            <h3>{{ plan.plan }}</h3>
            <div class="gradient"></div>
            <h2>{{ plan.price }}</h2>
            <base-button :title="'Get started'" @click="togglePlanPop(index)" class="b-btn z-[10]" />
            <div class="gradient"></div>
            <div class="pros">
              <div class="pro-wrap" v-for="(pro, index) in plan.packages" :key="index">
                <fa-icon :icon="['fas', 'arrow-right']" size="2xs" class="icon" />
                <p>{{ pro }}</p>
              </div>
            </div>
            <img v-lazy="{ src: srcPath }" class="gradient">
            <div v-if="plan.showPlanPop" class="plan-pop z-50">
              <button class="close-btn" @click="togglePlanPop(index)">X</button>
              <h3 class="text-[40px]"> VPN USAGE </h3>
              <p class="text-[30px]">Whop page MAY not load while using your local network IP address. Kindly
                activate your <a class="underline z-30 relative" href='https://protonvpn.com/'>VPN</a> to access
                the whop page.</p>
                <div class="payOn">
                <div v-for="(option, optionIndex) in plan.payOn" :key="optionIndex">
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
              <base-button :title="'Continue'" :link="selectedPaymentLink" class="b-btn z-50" />
              <div></div>
              <img src="../assets/icon/middle-gradient.png" alt="gradient"
                class="absolute bottom-0 top-0 z-20 opacity-[0.3]" />
            </div>
            <img src="../assets/icon/middle-gradient.png" alt="gradient"
              class="absolute bottom-10 z-20 opacity-[0.3]" />
          </div>
        </div>
      </div>
    </div>
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
          plan: 'FXT Signal Course',
          price: '$25',
          link: 'https://whop.com/checkout/plan_zd2m8IWnAKVae?d2c=true',
          packages: [
            'One - Three Trades per week',
            'Trading tutorial course',
            'Live News trading with Ken Jay',
            'Access to FXT community',
            '10% discount on advanced course',
            '1 month subscription',
          ],
          showPlanPop: false,
          payOn: [
            {
              name: "DOLLAR CARD/CRYPTO",
              img: paystack,
              link: "https://whop.com/checkout/plan_zd2m8IWnAKVae?d2c=true"
            }
          ]
        },
        {
          rating: 'MORE POPULAR',
          plan: 'FXT Beginners Course',
          price: '$50',
          link: 'https://whop.com/checkout/plan_FtTRe1q9Pc7in?d2c=true',
          packages: [
            'Recorded beginners crash course',
            'One of FXT setup',
            'Weekly Webinars',
            'Access to FXT community',
            '20% discount on advanced course',
            'Lifetime Mentorship',
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
          plan: 'FXT Advanced Course',
          price: '$200',
          link: 'https://whop.com/checkout/plan_Bv0a0lQnVaLlA?d2c=true',
          packages: [
            'Recorded crash courses',
            'All of FXT setup',
            'Live trading with Ken Jay',
            'Access to FXT community',
            'One of FXT Merch',
            'Lifetime Mentorship',
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

          .plan-pop {
            @apply p-8 flex flex-col items-center justify-between rounded-3xl bg-[#191919] text-white absolute bottom-0 left-0 right-0 top-0;

            .close-btn {
              @apply absolute top-2 right-2 text-black font-bold text-lg bg-[#AFAFAF] rounded-full w-8 h-8 flex items-center justify-center z-30;
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

          .payOn {
            @apply flex justify-center w-full gap-8
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
