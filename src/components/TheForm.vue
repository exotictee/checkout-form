<template>
    <div class="flex items-center justify-center h-screen">
        <section class="antialiased bg-gray-300 text-gray-600  p-4">
            <div class="h-full">
                <!-- Pay component -->
                <div>
                    <!-- Card background -->
                    <div class="relative px-4 sm:px-6 lg:px-8 max-w-lg mx-auto">
                        <img class="rounded-t shadow-lg" src="https://preview.cruip.com/mosaic/images/pay-bg.jpg"
                            width="460" height="180" alt="Pay background" />
                    </div>
                    <!-- Card body -->
                    <div class="relative px-4 sm:px-6 lg:px-8 pb-8 max-w-lg mx-auto">
                        <div class="bg-white px-8 pb-6 rounded-b shadow-lg">
                            <!-- Card header -->
                            <div class="text-center mb-6">
                                <div class="mb-2">
                                    <img class="-mt-8 inline-flex rounded-full"
                                        src="https://preview.cruip.com/mosaic/images/user-64-13.jpg" width="64" height="64"
                                        alt="User" />
                                </div>
                                <h1 class="text-xl leading-snug text-gray-800 font-semibold mb-2">
                                    Front-End Learning 🔥
                                </h1>
                                <div class="text-sm">
                                    Learn how to create real web apps using HTML & CSS. Code templates
                                    included.
                                </div>
                            </div>

                            <!-- Toggle -->
                            <div class="flex justify-center mb-6">
                                <div class="relative flex w-full p-1 bg-gray-50 rounded">
                                    <span class="absolute inset-0 m-1 pointer-events-none" aria-hidden="true">
                                        <span
                                            class="absolute inset-0 w-1/2 bg-cyan-500 rounded border border-gray-200 shadow-sm transform transition duration-150 ease-in-out"
                                            :class="{ 'translate-x-0': card, 'translate-x-full': !card }"></span>
                                    </span>
                                    <button
                                        class="relative flex-1 text-sm font-medium p-1 transition duration-150 ease-in-out focus:outline-none focus-visible:ring-2"
                                        @click="card = true">
                                        Pay With Card
                                    </button>
                                    <button
                                        class="relative flex-1 text-sm font-medium p-1 transition duration-150 ease-in-out focus:outline-none focus-visible:ring-2"
                                        @click="card = false">
                                        Pay With PayPal
                                    </button>
                                </div>
                            </div>

                            <!-- Card form -->
                            <div v-if="card">
                                <div class="space-y-4">
                                    <!-- Card Number -->
                                    <div>
                                        <label class="block text-sm font-medium mb-1" for="card-nr">
                                            Card Number <span class="text-red-500">*</span>
                                        </label>
                                        <input id="card-nr" ref="cardNumberInput"
                                            class="text-sm text-gray-800 bg-white border rounded leading-5 py-2 px-3 border-gray-200 hover:border-gray-300 focus:border-indigo-300 shadow-sm placeholder-gray-400 focus:ring-0 w-full"
                                            type="text" placeholder="1234 1234 1234 1234" v-model="formData.cardNumber" />
                                    </div>
                                    <!-- Expiry and CVC -->
                                    <div class="flex space-x-4">
                                        <div class="flex-1">
                                            <label class="block text-sm font-medium mb-1" for="card-expiry">
                                                Expiry Date <span class="text-red-500">*</span>
                                            </label>
                                            <input id="card-expiry"
                                                class="text-sm text-gray-800 bg-white border rounded leading-5 py-2 px-3 border-gray-200 hover:border-gray-300 focus:border-indigo-300 shadow-sm placeholder-gray-400 focus:ring-0 w-full"
                                                type="text" placeholder="MM/YY" v-model="formData.expiryDate"
                                                @input="formatExpiryDate" />
                                        </div>
                                        <div class="flex-1">
                                            <label class="block text-sm font-medium mb-1" for="card-cvc">
                                                CVC <span class="text-red-500">*</span>
                                            </label>
                                            <input id="card-cvc"
                                                class="text-sm text-gray-800 bg-white border rounded leading-5 py-2 px-3 border-gray-200 hover:border-gray-300 focus:border-indigo-300 shadow-sm placeholder-gray-400 focus:ring-0 w-full"
                                                type="text" placeholder="CVC" v-model="formData.cvc" />
                                        </div>
                                    </div>
                                    <!-- Name on Card -->
                                    <div>
                                        <label class="block text-sm font-medium mb-1" for="card-name">
                                            Name on Card <span class="text-red-500">*</span>
                                        </label>
                                        <input id="card-name"
                                            class="text-sm text-gray-800 bg-white border rounded leading-5 py-2 px-3 border-gray-200 hover:border-gray-300 focus:border-indigo-300 shadow-sm placeholder-gray-400 focus:ring-0 w-full"
                                            type="text" placeholder="Timilehin" v-model="formData.cardName" />
                                    </div>
                                    <!-- Email -->
                                    <div>
                                        <label class="block text-sm font-medium mb-1" for="card-email">
                                            Email <span class="text-red-500">*</span>
                                        </label>
                                        <input id="card-email"
                                            class="text-sm text-gray-800 bg-white border rounded leading-5 py-2 px-3 border-gray-200 hover:border-gray-300 focus:border-indigo-300 shadow-sm placeholder-gray-400 focus:ring-0 w-full"
                                            type="email" placeholder="timi@example.com" v-model="formData.email" />
                                    </div>
                                </div>
                                <!-- Form footer -->
                                <div class="mt-6">
                                    <div class="mb-4">
                                        <button
                                            class="font-medium text-sm inline-flex items-center justify-center px-3 py-2 border border-transparent rounded leading-5 shadow-sm transition duration-150 ease-in-out w-full bg-indigo-500 hover:bg-indigo-600 text-white focus:outline-none focus-visible:ring-2"
                                            @click="handlePayment">
                                            Pay $253.00
                                        </button>
                                    </div>
                                    <div class="text-xs text-gray-500 italic text-center">
                                        You'll be charged $253, including $48 for VAT in Italy
                                    </div>
                                </div>
                            </div>

                            <!-- PayPal form -->
                            <div v-else>
                                <div>
                                    <div class="mb-4">
                                        <button
                                            class="font-medium text-sm inline-flex items-center justify-center px-3 py-2 border border-transparent rounded leading-5 shadow-sm transition duration-150 ease-in-out w-full bg-indigo-500 hover:bg-indigo-600 text-white focus:outline-none focus-visible:ring-2">
                                            Pay with PayPal - $253.00
                                        </button>
                                    </div>
                                    <div class="text-xs text-gray-500 italic text-center">
                                        You'll be charged $253, including $48 for VAT in Italy
                                    </div>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </section>
    </div>
</template>
  

<script>
export default {
    data() {
        return {
            card: true,
            formData: {
                cardNumber: "",
                expiryDate: "",
                cvc: "",
                cardName: "",
                email: "",
            },
        };
    },
    methods: {
        handlePayment() {
            const requiredFields = [
                "cardNumber",
                "expiryDate",
                "cvc",
                "cardName",
                "email",
            ];

            // Check if any required field is empty
            const emptyFields = requiredFields.filter(
                (field) => !this.formData[field].trim()
            );

            if (emptyFields.length > 0) {
                alert("Fill in the required details");
                return;
            }

            // Verify the email format
            const emailPattern = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
            const isValidEmail = emailPattern.test(this.formData.email);

            if (!isValidEmail) {
                alert("Invalid email format");
                return;
            }

            // Email validation - For demonstration purposes, let's assume the email doesn't exist
            const isEmailExists = false;

            if (!isEmailExists) {
                alert("The email doesn't exist");
                return;
            }

            alert("Payment successful");
        },
        formatExpiryDate(event) {
            const input = event.target;
            const sanitizedValue = input.value.replace(/[^0-9]/g, "");
            let formattedValue = "";

            if (sanitizedValue.length > 0) {
                formattedValue += sanitizedValue.substr(0, 2);
            }

            if (sanitizedValue.length > 2) {
                formattedValue += "/" + sanitizedValue.substr(2, 2);
            }

            this.formData.expiryDate = formattedValue;
        },
    },
};
</script>

  