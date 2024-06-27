<script>
import 'boxicons'
</script>

<template>
    <header class="border-b-2 border-black pb-2 p-3">
        Chat from Chrome incognito
    </header>
    <div class="flex flex-col w-full relative h-[95%]">
        <div class="absolute overflow-y-auto max-h-full w-full flex flex-col">
            <div class="my-3 mx-2 max-w-full text-right justify-end">
                <div class="bg-[#37bb4f] float-end max-w-6xl px-3 pt-2 rounded-lg">
                    <div>Lorem ipsum dolor sit amet consectetur adipisicing elit. Ipsum, nobis.</div>
                    <div class="flex text-right float-end">
                        <p class="text-gray-600 text-sm p-1">08:00</p>
                        <box-icon color="blue" name='check-double'></box-icon>
                    </div>
                </div>
            </div>
            <div class="my-3 mx-2 max-w-full text-left justify-start">
                <div class="bg-[#a7a7aa] float-start max-w-6xl px-3 pt-2 rounded-lg">
                    <div>
                        Lorem ipsum dolor sit amet, consectetur adipisicing elit. Eos exercitationem iusto assumenda, eligendi beatae perferendis consequuntur. Aperiam voluptas vitae eius officia maiores tenetur deserunt iste temporibus ad neque necessitatibus ipsa odio non accusantium eos assumenda distinctio, laudantium quae. Atque, dicta incidunt iure sequi rerum neque nesciunt ea odio eum provident.
                    </div>
                    <div class="flex text-left float-start">
                        <p class="text-gray-600 text-sm p-1">08:00</p>
                        <box-icon color="blue" name='check-double'></box-icon>
                    </div>
                </div>
            </div>
        </div>
    </div>
    <footer class="w-full relative">
        <div class="absolute">
            <input type="text" name="Arifin" id="Arifin" class="w-full fixed bottom-0 h-12 border-t-2 border-black">
        </div>
    </footer>
</template>

<style></style>