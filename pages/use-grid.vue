<template>
    <div class="grid grid-cols-3 ... grid-flow-row-dense justify-items-center">
      <div class="bg-fuchsia-500 p-4">01</div>
      <div class="bg-fuchsia-500 p-4 justify-self-start">02</div>
      <div class="grid grid-rows-subgrid gap-4 row-span-3">
        <div class="bg-fuchsia-500 p-4 col-span-2 row-start-2">03</div>
      </div>
      <div class="bg-fuchsia-500 p-4">04</div>
      <div class="bg-fuchsia-500 p-4 col-start-1 col-end-3">05</div>
    </div>
  </template>