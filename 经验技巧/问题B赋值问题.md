---
title: 问题 B 赋值问题
date: 2017-05-03 16:10:02
tags:
categories: oj
---

## 题目描述

设有N个正整数(N<=20)，将它们联成一排，组成一个最大的多位整数。 例如：N=3时，3个整数13、312、343联成的最大整数为：34331213； 又如：N=4时，4个整数7，13，4，246联成的最大整数为：7424613；

## 输入

输入由多行组成，每一行的内容为： N N个整数

## 输出

对每一行的输入，输出一行结果，结果为这一行的N个整数可联成的最大整数。

## 样例输入

3 13 312 3434 7 13 4 246

## 样例输出

343312137424613

## 提示

<!--more-->

直接上代码：

```java
package fivethree;

import java.util.Scanner;
import java.lang.*;
import java.math.BigDecimal;

import javax.xml.transform.Templates;

public class maxnumber {
	
	public static String[] allString = new String[20];
	public static String[] allString2 = new String[20]; 
	public static StringBuffer[] allstringbuffer = new StringBuffer[20];
	public static StringBuffer[] allstringbuffer2 = new StringBuffer[20];

	maxnumber instance = new maxnumber();
	static Scanner in = new Scanner(System.in);
	
	public static String finalmaxnumber = "";
	public static void main (String argv[]){
		while(in.hasNext()){
			int n;
			n = in.nextInt();
			finalmaxnumber = "";
			int length;
			int max = 0;
			for(int i = 0;i < n;i++){
				String stringnumber = in.next();
				allString[i] = new String(stringnumber);
				allString2[i] = new String(stringnumber);
				allstringbuffer[i] = new StringBuffer(stringnumber);
				allstringbuffer2[i] = new StringBuffer(stringnumber);
				length = stringnumber.length();
				if(length >= max)
					max = length;
				//System.out.println("最大长度为" + max);
			}
			for(int i =0;i<n ;i++){
				char tempfinal = allString2[i].charAt(allString2[i].length()-1);
				int length2 =allString2[i].length();
				//System.out.println("最后一位是：" + tempfinal + "字符数组大小为：" + length2);
				for(int j = length2;j< max;j++){
					allstringbuffer2[i].append(tempfinal);
				}
				allString2[i] = new String(allstringbuffer2[i]);
			}
			
			/*for(int i =0;i<n;i++){
				System.out.println(allString2[i]);
			}*/
			
			String temp;
			String temp2;
			for(int i =0 ;i<n-1;i++){
				for(int j =0;j<n-i-1;j++){
					//System.out.println(Integer.parseInt(allString2[j]) + " and " +Integer.parseInt(allString2[j+1]));
					if(allString2[j].compareTo(allString2[j+1])>0){
						temp = allString[j];
						temp2= allString2[j];
						allString[j] = allString[j+1];
						allString2[j] = allString2[j+1];
						allString2[j+1] = temp2;
						allString[j+1] = temp;
					}
				}
			}
			/*System.out.println("allstring2");
			for(int i =0;i<n;i++){
				System.out.println(allString2[i]);
			}
			System.out.println("allstring");
			for(int i =0;i<n;i++){
				System.out.println(allString[i]);
			}*/
			for(int i=0;i<n;i++){
				finalmaxnumber = allString[i] + finalmaxnumber;
			}
			
			//int finalnumber = Integer.parseInt(finalmaxnumber);
			//BigDecimal finalnumber = BigDecimal.parseInt(finalmaxnumber);
			System.out.println(finalmaxnumber);	
		}

		
	}
	

}
```

