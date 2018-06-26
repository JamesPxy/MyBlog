---
layout: post
title: "RecycleView局部刷新"
date:   2018-6-26 11:27 +0800
categories: Android
tag: RecycleView
---

* content
{:toc}

1.第一种方法：
--------------

    public final void notifyItemChanged(int position, Object payload) {
            mObservable.notifyItemRangeChanged(position, 1, payload);
        }


 	public void onBindViewHolder(VH holder, int position, List<Object> payloads) {
            onBindViewHolder(holder, position);
    }

 关键点：在于payload 传递数据源  实现三参数的onBindViewHolder，如果payloads为空则全部刷新，不为空实现局部刷新


1.第二种方法：
--------------

     RecyclerView.ViewHolder viewHolder = recyclerView.findViewHolderForAdapterPosition(position);

     if (viewHolder != null && viewHolder instanceof DynamicNormalItemHolder) {
            DynamicNormalItemHolder holder= (DynamicNormalItemHolder) viewHolder;
            holder.setDynamicDetailContentText();
        }