---
title: ArrayBuffer转换
date: 2020/7/20 21:22:23
tags: [JavaScript]
categories: JavaScript
---

最近开发支付宝小程序蓝牙相关功能，由于支付宝小程序和微信小程序api设计有些不同，需要在 base64, ArrayBuffer, 16进制字符串直接进行转换，记录一下

```ts
import { Base64 } from 'js-base64';

export function arrayBufferToBase64(buffer: ArrayBuffer): string {
  return Base64.btoa(String.fromCharCode(...new Uint8Array(buffer)));
}

export function base64ToArrayBuffer(base64: string): ArrayBuffer {
  const binaryString = Base64.atob(base64);
  const len = binaryString.length;
  const bytes = new Uint8Array(len);
  for (let i = 0; i < len; i++) {
    bytes[i] = binaryString.charCodeAt(i);
  }
  return bytes.buffer;
}

export function buffer2Hex(buffer: ArrayBuffer): string {
  const hexArr = Array.prototype.map.call(new Uint8Array(buffer), function (bit) {
    return ('00' + bit.toString(16)).slice(-2);
  });
  return hexArr.join('');
}

export function hex2Buffer(hexStr: string): ArrayBuffer {
  const Uint8Numbers = hexStr.match(/../g).map((x) => Number('0x' + x));
  return new Uint8Array(Uint8Numbers).buffer;
}


```