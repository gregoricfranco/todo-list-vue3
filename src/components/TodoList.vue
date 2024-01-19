<template>
    <div id="toast-simple" v-show="isShow"
        class="flex items-center  fixed bottom-5 right-5 w-full max-w-xs p-4 space-x-4 rtl:space-x-reverse text-gray-500 bg-white divide-x rtl:divide-x-reverse divide-gray-200 rounded-lg shadow dark:text-gray-400 dark:divide-gray-700 space-x dark:bg-gray-800"
        role="alert">
        <svg class="w-5 h-5 text-blue-600 dark:text-blue-500 rotate-45" aria-hidden="true"
            xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 18 20">
            <path stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
                d="m9 17 8 2L9 1 1 19l8-2Zm0 0V9" />
        </svg>
        <div class="ps-4 text-sm font-normal">{{ mensagemToast }}</div>
    </div>

    <!-- Main modal -->
    <div id="crud-modal" tabindex="-1" aria-hidden="true"
        class="hidden overflow-y-auto overflow-x-hidden fixed top-0 right-0 left-0 z-50 justify-center items-center w-full md:inset-0 h-[calc(100%-1rem)] max-h-full">
        <div class="relative p-4 w-full max-w-md max-h-full">
            <!-- Modal content -->
            <div class="relative bg-white rounded-lg shadow dark:bg-gray-700">
                <!-- Modal header -->
                <div class="flex items-center justify-between p-4 md:p-5 border-b rounded-t dark:border-gray-600">
                    <h3 class="text-lg font-semibold text-gray-900 dark:text-white">
                        Novo Registro
                    </h3>
                    <button type="button"
                        class="text-gray-400 bg-transparent hover:bg-gray-200 hover:text-gray-900 rounded-lg text-sm w-8 h-8 ms-auto inline-flex justify-center items-center dark:hover:bg-gray-600 dark:hover:text-white"
                        data-modal-toggle="crud-modal">
                        <svg class="w-3 h-3" aria-hidden="true" xmlns="http://www.w3.org/2000/svg" fill="none"
                            viewBox="0 0 14 14">
                            <path stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
                                d="m1 1 6 6m0 0 6 6M7 7l6-6M7 7l-6 6" />
                        </svg>
                        <span class="sr-only">Close modal</span>
                    </button>
                </div>
                <!-- Modal body -->
                <form class="p-4 md:p-5" @submit.prevent="salvar">
                    <div class="grid gap-4 mb-4 grid-cols-2">
                        <div class="col-span-2 sm:col-span-1">
                            <label for="name"
                                class="block mb-2 text-sm font-medium text-gray-900 dark:text-white">Name</label>
                            <input type="text" v-model="pessoa.nome" name="name" id="name"
                                class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-primary-600 focus:border-primary-600 block w-full p-2.5 dark:bg-gray-600 dark:border-gray-500 dark:placeholder-gray-400 dark:text-white dark:focus:ring-primary-500 dark:focus:border-primary-500"
                                placeholder="Nome Completo" required="">
                        </div>
                        <div class="col-span-2 sm:col-span-1">
                            <label for="name"
                                class="block mb-2 text-sm font-medium text-gray-900 dark:text-white">Idade</label>
                            <input type="number" v-model="pessoa.idade"
                                class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-primary-600 focus:border-primary-600 block w-full p-2.5 dark:bg-gray-600 dark:border-gray-500 dark:placeholder-gray-400 dark:text-white dark:focus:ring-primary-500 dark:focus:border-primary-500"
                                placeholder="Idade" required="">
                        </div>
                        <div class="col-span-2 sm:col-span-1">
                            <label for="price"
                                class="block mb-2 text-sm font-medium text-gray-900 dark:text-white">Telefone</label>
                            <input type="number" v-model="pessoa.telefone"
                                class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-primary-600 focus:border-primary-600 block w-full p-2.5 dark:bg-gray-600 dark:border-gray-500 dark:placeholder-gray-400 dark:text-white dark:focus:ring-primary-500 dark:focus:border-primary-500"
                                placeholder="" required="">
                        </div>
                        <div class="col-span-2 sm:col-span-1">
                            <label for="category"
                                class="block mb-2 text-sm font-medium text-gray-900 dark:text-white">Categoria</label>
                            <select id="category" v-model="pessoa.categoria"
                                class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-primary-500 focus:border-primary-500 block w-full p-2.5 dark:bg-gray-600 dark:border-gray-500 dark:placeholder-gray-400 dark:text-white dark:focus:ring-primary-500 dark:focus:border-primary-500">
                                <option selected="">Selcione uma Categoria</option>
                                <option value="DEV">DEV</option>
                                <option value="Analista">Analista</option>
                                <option value="Tester">Tester</option>
                            </select>
                        </div>


                        <div class="col-span-2">
                            <div class="col-span-2">
                                <label for="name"
                                    class="block mb-2 text-sm font-medium text-gray-900 dark:text-white">Endereco</label>
                                <input type="text" v-model="pessoa.endereco"
                                    class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-primary-600 focus:border-primary-600 block w-full p-2.5 dark:bg-gray-600 dark:border-gray-500 dark:placeholder-gray-400 dark:text-white dark:focus:ring-primary-500 dark:focus:border-primary-500"
                                    placeholder="Endereco" required="">
                            </div>
                        </div>
                    </div>
                    <button type="submit"
                        class="text-white inline-flex items-center bg-blue-700 hover:bg-blue-800 focus:ring-4 focus:outline-none focus:ring-blue-300 font-medium rounded-lg text-sm px-5 py-2.5 text-center dark:bg-blue-600 dark:hover:bg-blue-700 dark:focus:ring-blue-800">
                        <svg class="me-1 -ms-1 w-5 h-5" fill="currentColor" viewBox="0 0 20 20"
                            xmlns="http://www.w3.org/2000/svg">
                            <path fill-rule="evenodd"
                                d="M10 5a1 1 0 011 1v3h3a1 1 0 110 2h-3v3a1 1 0 11-2 0v-3H6a1 1 0 110-2h3V6a1 1 0 011-1z"
                                clip-rule="evenodd"></path>
                        </svg>
                        Add
                    </button>
                </form>
            </div>
        </div>
    </div>


    <section class="flex items-center">
        <div class="w-full">
            <!-- Start coding here -->
            <div class="relative bg-white shadow-md dark:bg-gray-800 sm:rounded-lg">
                <div class="flex flex-col items-center justify-between p-4 space-y-3 md:flex-row md:space-y-0 md:space-x-4">
                    <div class="w-full md:w-1/2">
                        <form class="flex items-center">
                            <label for="simple-search" class="sr-only">Search</label>
                            <div class="relative w-full">
                                <div class="absolute inset-y-0 left-0 flex items-center pl-3 pointer-events-none">
                                    <svg aria-hidden="true" class="w-5 h-5 text-gray-500 dark:text-gray-400"
                                        fill="currentColor" viewbox="0 0 20 20" xmlns="http://www.w3.org/2000/svg">
                                        <path fill-rule="evenodd"
                                            d="M8 4a4 4 0 100 8 4 4 0 000-8zM2 8a6 6 0 1110.89 3.476l4.817 4.817a1 1 0 01-1.414 1.414l-4.816-4.816A6 6 0 012 8z"
                                            clip-rule="evenodd" />
                                    </svg>
                                </div>
                                <input type="text" v-model="buscarPor" id="simple-search"
                                    class="block w-full p-2 pl-10 text-sm text-gray-900 border border-gray-300 rounded-lg bg-gray-50 focus:ring-primary-500 focus:border-primary-500 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-primary-500 dark:focus:border-primary-500"
                                    placeholder="Search" required="">
                            </div>
                        </form>
                    </div>
                    <div
                        class="flex flex-col items-stretch justify-end flex-shrink-0 w-full space-y-2 md:w-auto md:flex-row md:space-y-0 md:items-center md:space-x-3">

                        <button data-modal-target="crud-modal" data-modal-toggle="crud-modal"
                            class="block text-white bg-blue-700 hover:bg-blue-800 focus:ring-4 focus:outline-none focus:ring-blue-300 font-medium rounded-lg text-sm px-5 py-2.5 text-center dark:bg-blue-600 dark:hover:bg-blue-700 dark:focus:ring-blue-800"
                            type="button">
                            Novo Registro
                        </button>

                        <div class="flex items-center w-full space-x-3 md:w-auto">

                            <button id="actionsDropdownButton" data-dropdown-toggle="actionsDropdown"
                                class="flex items-center justify-center w-full px-4 py-2 text-sm font-medium text-gray-900 bg-white border border-gray-200 rounded-lg md:w-auto focus:outline-none hover:bg-gray-100 hover:text-primary-700 focus:z-10 focus:ring-4 focus:ring-gray-200 dark:focus:ring-gray-700 dark:bg-gray-800 dark:text-gray-400 dark:border-gray-600 dark:hover:text-white dark:hover:bg-gray-700"
                                type="button">
                                Acoes
                                <svg class="-mr-1 ml-1.5 w-5 h-5" fill="currentColor" viewbox="0 0 20 20"
                                    xmlns="http://www.w3.org/2000/svg" aria-hidden="true">
                                    <path clip-rule="evenodd" fill-rule="evenodd"
                                        d="M5.293 7.293a1 1 0 011.414 0L10 10.586l3.293-3.293a1 1 0 111.414 1.414l-4 4a1 1 0 01-1.414 0l-4-4a1 1 0 010-1.414z" />
                                </svg>
                            </button>

                            <div id="actionsDropdown"
                                class="z-10 hidden bg-white divide-y divide-gray-100 rounded shadow w-44 dark:bg-gray-700 dark:divide-gray-600">
                                <ul class="py-1 text-sm text-gray-700 dark:text-gray-200"
                                    aria-labelledby="actionsDropdownButton">
                                    <li>
                                        <a href="#" @click="editTodos()" v-if="!isEdit"
                                            class="block px-4 py-2 hover:bg-gray-100 dark:hover:bg-gray-600 dark:hover:text-white">Editar
                                            Todos</a>
                                        <a href="#" @click="editTodos()" v-else
                                            class="block px-4 py-2 hover:bg-gray-100 dark:hover:bg-gray-600 dark:hover:text-white">Salvar
                                            Edicao</a>
                                    </li>
                                </ul>
                                <div class="py-1">

                                    <a href="#" @click="todos()"
                                        class="block px-4 py-2 text-sm text-gray-700 hover:bg-gray-100 dark:hover:bg-gray-600 dark:text-gray-200 dark:hover:text-white">
                                        Selecionar Todos
                                        <span
                                            class="inline-flex items-center justify-center w-4 h-4 ms-2 text-xs font-semibold text-blue-800 bg-blue-200 rounded-full">
                                            {{ quantidadeSelecionados }}
                                        </span>
                                    </a>
                                    <a href="#" v-show="quantidadeSelecionados > 0" @click="deletarTodos()"
                                        class="block px-4 py-2 text-sm text-gray-700 hover:bg-gray-100 dark:hover:bg-gray-600 dark:text-gray-200 dark:hover:text-white">
                                        Deletar Todos</a>
                                </div>
                            </div>
                            <button id="dropdownBgHoverButton" data-dropdown-toggle="dropdownBgHover"
                                class="text-white bg-blue-700 hover:bg-blue-800 focus:ring-4 focus:outline-none focus:ring-blue-300 font-medium rounded-lg text-sm px-5 py-2.5 text-center inline-flex items-center dark:bg-blue-600 dark:hover:bg-blue-700 dark:focus:ring-blue-800"
                                type="button">Filtrar Categorias <svg class="w-2.5 h-2.5 ms-3" aria-hidden="true"
                                    xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 10 6">

                                    <path stroke="currentColor" stroke-linecap="round" stroke-linejoin="round"
                                        stroke-width="2" d="m1 1 4 4 4-4" />
                                </svg>
                            </button>
                            <!-- Dropdown menu -->
                            <div id="dropdownBgHover" class="z-10 hidden w-48 bg-white rounded-lg shadow dark:bg-gray-700">

                                <input type="text"  v-model="categoriaSearch" id="table-search"
                                    class="block  m-2 text-sm text-gray-900 border border-gray-300 rounded-lg bg-gray-50 focus:ring-blue-500 focus:border-blue-500 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500"
                                    placeholder="Procure as Categorias">

                                <ul v-for="(categoria, index) in buscarCategoria" :key="categoria.index"
                                    class="p-3 space-y-1 text-sm text-gray-700 dark:text-gray-200"
                                    aria-labelledby="dropdownBgHoverButton">
                                    <li>
                                        <div class="flex items-center p-2 rounded hover:bg-gray-100 dark:hover:bg-gray-600">
                                            <input :id="categoria" v-model="checkedCategorias" type="checkbox"
                                                :value="categoria"
                                                class="w-4 h-4 text-blue-600 bg-gray-100 border-gray-300 rounded focus:ring-blue-500 dark:focus:ring-blue-600 dark:ring-offset-gray-700 dark:focus:ring-offset-gray-700 focus:ring-2 dark:bg-gray-600 dark:border-gray-500">
                                            <label for="checkbox-item-4"
                                                class="w-full ms-2 text-sm font-medium text-gray-900 rounded dark:text-gray-300">{{
                                                      categoria}}</label>
                                        </div>
                                    </li>
                                </ul>
                                <div class="py-2">
                                    <button @click="fintrarCategoria()"
                                        class="w-full text-white bg-gray-300 hover:bg-blue-800 focus:ring-4 focus:outline-none focus:ring-blue-300 font-medium rounded-lg text-sm px-5 py-2.5 text-center dark:bg-blue-600 dark:hover:bg-blue-700 dark:focus:ring-blue-800"
                                        type="button">
                                        Filtrar
                                    </button>

                                </div>
                            </div>
                            <!-- Dropdown menu -->
                            <div id="filterDropdown"
                                class="z-10 hidden w-48 p-3 bg-white rounded-lg shadow dark:bg-gray-700">
                                <h6 class="mb-3 text-sm font-medium text-gray-900 dark:text-white">
                                    Categoria
                                </h6>
                                <ul v-for="pessoa in listaPessoas" :key="pessoa.id"
                                    class="h-8 px-3 pb-3 overflow-y-auto text-sm text-gray-700 dark:text-gray-200"
                                    aria-labelledby="dropdownSearchButton">
                                    <li>
                                        <div
                                            class="flex items-center ps-2 rounded hover:bg-gray-100 dark:hover:bg-gray-600">
                                            <input id="checkbox-item-11" type="checkbox" value=""
                                                class="w-4 h-4 text-blue-600 bg-gray-100 border-gray-300 rounded focus:ring-blue-500 dark:focus:ring-blue-600 dark:ring-offset-gray-700 dark:focus:ring-offset-gray-700 focus:ring-2 dark:bg-gray-600 dark:border-gray-500">
                                            <label for="checkbox-item-11"
                                                class="w-full py-2 ms-2 text-sm font-medium text-gray-900 rounded dark:text-gray-300">{{
                                                    pessoa.categoria }}</label>
                                        </div>
                                    </li>

                                </ul>
                                <a href="#"
                                    class="flex items-center p-3 text-sm font-medium text-red-600 border-t border-gray-200 rounded-b-lg bg-gray-50 dark:border-gray-600 hover:bg-gray-100 dark:bg-gray-700 dark:hover:bg-gray-600 dark:text-red-500 hover:underline">

                                    Filtrar
                                </a>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </section>
    <hr class="m-3">
    <div class="relative overflow-x-auto shadow-md sm:rounded-lg">
        <table class="w-full text-sm text-left rtl:text-right text-gray-500 dark:text-gray-400">
            <thead class="text-xs text-gray-700 uppercase bg-gray-50 dark:bg-gray-700 dark:text-gray-400">
                <tr>
                    <th scope="col" class="p-4">
                        <div class="flex items-center">
                            <input id="checkbox-all-search" type="checkbox" @click="todos()"
                                class="w-4 h-4 text-blue-600 bg-gray-100 border-gray-300 rounded focus:ring-blue-500 dark:focus:ring-blue-600 dark:ring-offset-gray-800 dark:focus:ring-offset-gray-800 focus:ring-2 dark:bg-gray-700 dark:border-gray-600">
                            <label for="checkbox-all-search" class="sr-only">checkbox</label>
                        </div>
                    </th>
                    <th scope="col" class="px-6 py-3">
                        Nome
                    </th>
                    <th scope="col" class="px-6 py-3">
                        Telefone
                    </th>
                    <th scope="col" class="px-6 py-3">
                        Endereco
                    </th>
                    <th scope="col" class="px-6 py-3" @click="sortUsersByAge()">
                        <div class="flex items-center">
                            Idade
                            <svg class="w-3 h-3 ms-1.5" aria-hidden="true" xmlns="http://www.w3.org/2000/svg"
                                fill="currentColor" viewBox="0 0 24 24">
                                <path
                                    d="M8.574 11.024h6.852a2.075 2.075 0 0 0 1.847-1.086 1.9 1.9 0 0 0-.11-1.986L13.736 2.9a2.122 2.122 0 0 0-3.472 0L6.837 7.952a1.9 1.9 0 0 0-.11 1.986 2.074 2.074 0 0 0 1.847 1.086Zm6.852 1.952H8.574a2.072 2.072 0 0 0-1.847 1.087 1.9 1.9 0 0 0 .11 1.985l3.426 5.05a2.123 2.123 0 0 0 3.472 0l3.427-5.05a1.9 1.9 0 0 0 .11-1.985 2.074 2.074 0 0 0-1.846-1.087Z" />
                            </svg>
                        </div>
                    </th>

                    <th scope="col" class="px-6 py-3">
                        Categoria
                    </th>
                    <th scope="col" class="px-6 py-3">
                        Action
                    </th>
                </tr>
            </thead>
            <tbody>
                <tr v-for="(pessoa, index) in buscar" :key="index"
                    class="odd:bg-white odd:dark:bg-gray-900 even:bg-gray-50 even:dark:bg-gray-800 border-b dark:border-gray-700">
                    <td class="w-4 p-4">
                        <div class="flex items-center">
                            <input id="checkbox-table-search-1" v-model="pessoa.selected" type="checkbox"
                                class="w-4 h-4 text-blue-600 bg-gray-100 border-gray-300 rounded focus:ring-blue-500 dark:focus:ring-blue-600 dark:ring-offset-gray-800 dark:focus:ring-offset-gray-800 focus:ring-2 dark:bg-gray-700 dark:border-gray-600">
                            <label for="checkbox-table-search-1" class="sr-only">checkbox</label>
                        </div>
                    </td>
                    <th scope="row" class="px-6 py-4 font-medium text-gray-900 whitespace-nowrap dark:text-white">
                        <span v-if="!pessoa.selected">{{ pessoa.nome }}</span>
                        <input type="text" v-else v-model="pessoa.nome" id="table-search"
                            class="block   text-sm text-gray-900 border border-gray-300 rounded-lg bg-gray-50 focus:ring-blue-500 focus:border-blue-500 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500"
                            placeholder="Search for items">
                    </th>
                    <td class="px-6 py-4">
                        <span v-if="!pessoa.selected">{{ pessoa.telefone }}</span>
                        <input type="text" v-else v-model="pessoa.telefone" id="table-search"
                            class="block  text-sm text-gray-900 border border-gray-300 rounded-lg bg-gray-50 focus:ring-blue-500 focus:border-blue-500 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500"
                            placeholder="Search for items">

                    </td>
                    <td class="px-6 py-4">
                        <span v-if="!pessoa.selected">{{ pessoa.endereco }}</span>
                        <input type="text" v-else v-model="pessoa.endereco" id="table-search"
                            class="block p-2 ps-10 text-sm text-gray-900 border border-gray-300 rounded-lg bg-gray-50 focus:ring-blue-500 focus:border-blue-500 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500"
                            placeholder="Search for items">

                    </td>
                    <td>
                        <span v-if="!pessoa.editando">{{ pessoa.idade }}</span>
                        <input type="text" v-else v-model="pessoa.idade" id="table-search"
                            class="block p-2 ps-10 text-sm text-gray-900 border border-gray-300 rounded-lg bg-gray-50 focus:ring-blue-500 focus:border-blue-500 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500"
                            placeholder="Search for items">

                    </td>
                    <td class="px-6 py-4">
                        {{ pessoa.categoria }}
                    </td>
                    <td>
                        <div class="inline-flex rounded-md shadow-sm" role="group">
                            <button type="button" @click="editarItem(pessoa)" v-if="!pessoa.editando"
                                class="inline-flex items-center px-4 py-2 text-sm font-medium text-gray-900 bg-white border border-gray-200 rounded-s-lg hover:bg-gray-100 hover:text-blue-700 focus:z-10 focus:ring-2 focus:ring-blue-700 focus:text-blue-700 dark:bg-gray-700 dark:border-gray-600 dark:text-white dark:hover:text-white dark:hover:bg-gray-600 dark:focus:ring-blue-500 dark:focus:text-white">
                                <svg class="w-4 h-4 text-gray-800 dark:text-white" aria-hidden="true"
                                    xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 20 18">
                                    <path stroke="currentColor" stroke-linecap="round" stroke-linejoin="round"
                                        stroke-width="2"
                                        d="M4.109 17H1v-2a4 4 0 0 1 4-4h.87M10 4.5a3.5 3.5 0 1 1-7 0 3.5 3.5 0 0 1 7 0Zm7.95 2.55a2 2 0 0 1 0 2.829l-6.364 6.364-3.536.707.707-3.536 6.364-6.364a2 2 0 0 1 2.829 0Z" />
                                </svg>

                            </button>
                            <button type="button" @click="salvarEdicao(pessoa)" v-else
                                class="inline-flex items-center px-4 py-2 text-sm font-medium text-green-900 bg-white border-t border-b border-gray-200 hover:bg-gray-100 hover:text-green-700 focus:z-10 focus:ring-2 focus:ring-blue-700 focus:text-green-700 dark:bg-gray-700 dark:border-gray-600 dark:text-white dark:hover:text-white dark:hover:bg-gray-600 dark:focus:ring-blue-500 dark:focus:text-white">
                                <svg class="w-4 h-4 text-gray-800 dark:text-white" aria-hidden="true"
                                    xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 16 12">
                                    <path stroke="currentColor" stroke-linecap="round" stroke-linejoin="round"
                                        stroke-width="2" d="M1 5.917 5.724 10.5 15 1.5" />
                                </svg>

                            </button>

                            <button type="button" @click="deletar(index)"
                                class="inline-flex items-center px-4 py-2 text-sm font-medium text-gray-900 bg-white border border-gray-200 rounded-e-lg hover:bg-gray-100 hover:text-blue-700 focus:z-10 focus:ring-2 focus:ring-blue-700 focus:text-blue-700 dark:bg-gray-700 dark:border-gray-600 dark:text-white dark:hover:text-white dark:hover:bg-gray-600 dark:focus:ring-blue-500 dark:focus:text-white">
                                <svg class="w-4 h-4 text-gray-800 dark:text-white" aria-hidden="true"
                                    xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 18 20">
                                    <path stroke="currentColor" stroke-linecap="round" stroke-linejoin="round"
                                        stroke-width="2"
                                        d="M1 5h16M7 8v8m4-8v8M7 1h4a1 1 0 0 1 1 1v3H6V2a1 1 0 0 1 1-1ZM3 5h12v13a1 1 0 0 1-1 1H4a1 1 0 0 1-1-1V5Z" />
                                </svg>
                            </button>
                        </div>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
</template>

<script setup>
import { reactive, computed, onMounted, ref } from 'vue';

const pessoa = reactive({});
const listaPessoas = ref([])
const buscarPor = ref('');
const categoriaSearch = ref('');
const isShow = ref(false);
const isEdit = ref(false);
const isSort = ref(false);
const mensagemToast = ref('');
const quantidadeSelecionados = ref(0)
const listaCategorias = ref([])
const checkedCategorias = ref([])



function salvar() {
    console.log(pessoa)
    listaPessoas.value.push({
        nome: pessoa.nome,
        telefone: pessoa.telefone,
        endereco: pessoa.endereco,
        idade: pessoa.idade,
        categoria: pessoa.categoria
    })

    showToast("Criado com sucesso");
    limpar()

}

function popularLista() {
    listaPessoas.value = [
        {
            nome: "Maria",
            telefone: "48999999999",
            endereco: "Servidao dos Namorados, 144",
            categoria: "Dev",
            idade: 19
        },
        {
            nome: "Pedro",
            telefone: "48989988999",
            endereco: "Av Mauro Ramos",
            categoria: "Dev",
            idade: 22
        },
        {
            nome: "Felipe",
            telefone: "48999955976",
            endereco: "Rua Paulo Alvarez",
            categoria: "Analista",
            idade: 33
        },
        {
            nome: "Marcio",
            telefone: "47999999966",
            endereco: "Rodovia Amaro Fagundes",
            categoria: "Tester",
            idade: 18
        },
    ];
    listaCategorias.value = [...new Set(listaPessoas.value.map(item => item.categoria))];
}

function showToast(mensagemTxt) {

    isShow.value = true;
    mensagemToast.value = mensagemTxt
    setTimeout(() => {
        isShow.value = false;
    }
        , 3000);
}

const sortUsersByAge = () => {
    listaPessoas.value.sort((a, b) => {
        const directionMultiplier = isSort.value ? -1 : 1;
        return (a.idade - b.idade) * directionMultiplier;
    });
    isSort.value = !isSort.value;
}




function limpar() {
    pessoa.telefone = "";
    pessoa.nome = "";
    pessoa.endereco = "";
    pessoa.idade = "";
    pessoa.categoria = "";
}

const editarItem = (item) => {
    item.editando = true;
};

const salvarEdicao = (item) => {
    item.editando = false;
    showToast("Editado com sucesso");
};

const deletar = (index) => {
    listaPessoas.value.splice(index, 1)
};


const todos = () => {
    listaPessoas.value.forEach((pessoa, index) => {
        pessoa.selected = !pessoa.selected;
        quantidadeSelecionados.value = pessoa.selected ? index + 1 : 0;
    });
};

const deletarTodos = () => {
    for (let i = listaPessoas.value.length - 1; i >= 0; i--) {
        const pessoa = listaPessoas.value[i];
        if (pessoa.selected) {
            listaPessoas.value.splice(i, 1);
        }
    }
    quantidadeSelecionados.value = 0

};

const editTodos = () => {

    isEdit.value = !isEdit.value;

    // Atualiza a propriedade editando de cada pessoa
    listaPessoas.value.forEach(pessoa => {
        pessoa.selected = isEdit.value
        // pessoa.editando = isEdit.value
    })
};

const fintrarCategoria = () => {
    popularLista();
    if (checkedCategorias.value.length > 0) {
        const listaComum = listaPessoas.value.filter((item) => checkedCategorias.value.includes(item.categoria));
        listaPessoas.value = listaComum
    }

}

const buscar = computed(() => {
    return listaPessoas.value.filter(
        pessoa => pessoa.nome.toLowerCase().includes(buscarPor.value.toLowerCase()) ||
            pessoa.endereco.toLowerCase().includes(buscarPor.value.toLowerCase()) ||
            pessoa.idade === Number(buscarPor.value) ||
            pessoa.categoria.toLowerCase().includes(buscarPor.value.toLowerCase()) ||
            pessoa.telefone.toLowerCase().includes(buscarPor.value.toLowerCase())
    );
});

const buscarCategoria = computed(() =>{
    return listaCategorias.value.filter(
        categoria => categoria.toLowerCase().includes(categoriaSearch.value.toLowerCase())
    )
})

onMounted(() => {
    popularLista();
})

</script>
