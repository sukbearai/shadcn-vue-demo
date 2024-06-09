<script setup lang="ts">
import { ref } from 'vue'

import * as z from 'zod'
import { h } from 'vue'
import { Button } from '@/components/ui/button'
import { useToast } from '@/components/ui/toast/use-toast'
import { AutoForm } from '@/components/ui/auto-form'

import { cn } from '@@/lib/utils'
import IcBaselineWechat from '~icons/ic/baseline-wechat';
import LucideSpinner from '~icons/lucide/loader-2'

const { toast } = useToast()

const schema = z.object({
  username: z
    .string({
      required_error: '用户名必填',
    })
    .min(2, {
      message: '用户名必须至少有2个字符',
    }),

  password: z
    .string({
      required_error: '密码必填',
    })
    .min(8, {
      message: '密码必须至少有8个字符',
    })
})

const isLoading = ref(false)
async function onSubmit(values: Record<string, any>) {
  isLoading.value = true

  setTimeout(async () => {
    isLoading.value = false

    toast({
    title: '您提交了以下值',
    description: h('pre', { class: 'mt-2 w-[340px] rounded-md bg-slate-950 p-4' }, h('code', { class: 'text-white' }, JSON.stringify(values, null, 2)))})

  }, 1000)
}
</script>

<template>
  <div :class="cn('grid gap-6', $attrs.class ?? '')">
    <AutoForm
      class="space-y-6"
      :schema="schema"
      :field-config="{
        username: {
        label: '昵称',
        inputProps: {
          type: 'text',
          placeholder: '您的昵称',
          },
        },
        password: {
        label: '你的安全码',
        inputProps: {
          type: 'password',
          placeholder: '••••••••',
          },
        },
      }"
      @submit="onSubmit"
    >
      <Button type="submit">
        <LucideSpinner v-if="isLoading" class="mr-2 h-4 w-4 animate-spin" />
        登录
      </Button>
    </AutoForm>
    <div class="relative">
      <div class="absolute inset-0 flex items-center">
        <span class="w-full border-t" />
      </div>
      <div class="relative flex justify-center text-xs uppercase">
        <span class="bg-background px-2 text-muted-foreground">
          或继续
        </span>
      </div>
    </div>
     <Button variant="outline" type="button" :disabled="isLoading">
      <LucideSpinner v-if="isLoading" class="mr-2 h-4 w-4 animate-spin" />
      <IcBaselineWechat  v-else class="mr-2 h-4 w-4"/>
      微信
    </Button>
  </div>
</template>
