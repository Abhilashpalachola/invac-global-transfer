<template>
    <div class="w-full relative">
        <div class="w-full lg:h-screen lg:flex">
            <div class="lg:w-[50%] lg:min-w-[50%] lg:h-full px-10 pb-20 lg:pb-0 lg:px-20 pt-20 text-white">
                <NuxtLink to="/">
                    <img src="@/assets/images/logo.svg" class="h-7" alt="" />
                </NuxtLink>

                <p class="tracking-[0.6rem] text-xl mt-20 lg:mt-44">Contact Us</p>

                <h2 class="lg:mt-44 text-4xl mt-20 lg:text-6xl font-semibold">
                    <span class="text-[#FF7900]">Product</span>
                    <span class="block font-medium mt-3">Enquiry / Demo</span>
                </h2>
            </div>
            <div class="lg:w-[50%] bg-white text-black lg:min-w-[50%] h-full pt-14 pb-10 px-10 lg:px-20 grid">
                <div class="w-full flex justify-end items-center place-self-start min-h-fit max-h-fit">


                    <NuxtLink class="hidden lg:block" to="/">
                        <img src="@/assets/icons/x.svg" class="h-10 w-10" alt="" />
                    </NuxtLink>
                </div>

                
            </div>
        </div>

        <div v-if="submittedState"
            class="h-screen w-full font-semibold flex flex-col gap-y-6 justify-center items-center text-center fixed top-0 z-50 px-10 bg-white">
            <h3>
                <img src="@/assets/icons/logo-white.svg" class="h-7 lg:h-7 xl:h-8 2xl:h-9 animate-bounce duration-500"
                    alt="">
            </h3>
            <h3 class=" text-lg lg:text-xl text-black">Thank you</h3>
            <h3 class=" text-lg lg:text-xl text-black">
                Thank you, we will get back to you shortly.
            </h3>
        </div>
    </div>
</template>
  
<script setup>
useHead({
    title: `Experience InVac Central Vacuum System | Schedule Your Demo Now`,
    meta: [
        {
            name: 'description',
            content: `Explore the potential of our products by booking a demo now for an engaging interaction.`
        }
    ]
})


definePageMeta({
    scrollToTop: true,
    pageTransition: false,
});
const nameRef = ref("");
const emailRef = ref("");
const phoneRef = ref("");
const cityRef = ref("");
const typeOfHome = ref("apartment");
const sizeOfHome = ref("2000-sft");
const currentStage = ref("under-construction");
const router = useRouter()
const submittedState = ref(false)
const date = new Date()
const WEB3FORMS_ACCESS_KEY = "298883d0-8170-41ea-8f34-2663da8986c0";

const isNameValid = computed(() => nameRef.value ? /^[A-Za-z\s]+$/.test(nameRef.value) : true);
const isEmailValid = computed(() => emailRef.value ? /^[^\s@]+@[^\s@]+\.[^\s@]+$/.test(emailRef.value) : true);
const isPhoneValid = computed(() => phoneRef.value ? /^\d{10}$/.test(phoneRef.value) : true);
const isCityValid = computed(() => cityRef.value ? /^[A-Za-z\s]+$/.test(cityRef.value) : true);

const submitForm = async () => {
    const formData = {
        access_key: WEB3FORMS_ACCESS_KEY,
        name: nameRef.value,
        email: emailRef.value,
        phone: phoneRef.value,
        city: cityRef.value,
        typeOfHome: typeOfHome.value,
        sizeOfHome: sizeOfHome.value,
        currentStage: currentStage.value,
        currentDate: date
    };
    if (isNameValid._value && isEmailValid._value && isPhoneValid._value && isCityValid._value) {

        try {

            const response = await fetch("https://api.web3forms.com/submit", {
                method: "POST",
                headers: {
                    "Content-Type": "application/json",
                    Accept: "application/json",
                },
                body: JSON.stringify(formData),
            });
            const result = await response.json();
            if (result.success) {
                console.log(result);
            }
            submittedState.value = true
            submittedState.value = false
            router.push('/thank-you')

        }



        catch (error) {
            console.log(error.message)
        }
    }

};
</script>
  
<style scoped>
select {
    appearance: none;
}
</style>
  
