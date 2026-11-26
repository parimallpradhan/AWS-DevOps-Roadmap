# **Explain AWS S3 Storage Classes Using Amazon Prime Video**

Let's imagine we are DevOps Engineers working for a video-streaming platform like **Amazon Prime Video**.

Our responsibility is to store movies, web series, trailers and other video files in Amazon S3 while controlling storage costs.

**Imagine Prime Video has 10,000 movies. Does every customer watch all 10,000 movies every day?**

No!

- Some movies are watched millions of times.
- Some movies are watched occasionally.
- Some old movies are rarely watched.
- Some movies are retained for archival or business purposes.

So, why should the company pay the same storage price for every movie?

This is where **Amazon S3 Storage Classes** help.

## **1. Understand each S3 Storage Class with Prime Video**

[Baixe o aplicativo do Amazon Prime Video para Windows 10 | Produto](https://images.openai.com/static-rsc-4/9EQUJoXoMYDe1yqgB8e8n4vK7i2Dve3mEJwNFJjMZzhEEv9lhRcX18NqYNe8Qz9XE9kLkX3Q5TIxIQb5KzDRSE_u79P5Pdk1g6Cmy6Ef_xbbOG9sZUS2s7eFtaLF7eGhb85Ik1PKD-1rFCBPGWTgUuQ6cwvKqAfsyQdStyp_pSk?purpose=inline)

**S3 Standard – Frequently watched movies**

Example: Newly released movies and popular web series.

Customers watch these movies regularly, so the company needs fast access.

**Why?** Frequently accessed data.

[Amazonプライム・ビデオに「1980年代映画」っていうカテゴリーができてるぞ～！ | オモコロブロス！](https://images.openai.com/static-rsc-4/eyHGK634_5C5C6ENcc__Qd8SDFUFP0-j1WFF3WAB3PgNVRynppNrdgouNadiLdScG8JqDlf5TNDQeD3_p-wYxe0KBkPiz18_kx_XLNbOFyXLw17PkeDOMFjeieCwe9kT9PbXyJ4CGBbARcGhOTsBnr7kLJFiF2Rz34u7IDakbWI?purpose=inline)

**S3 Standard-IA – Occasionally watched movies**

Example: Movies released 6 months ago that customers watch occasionally.

They still need quick access, but are not watched frequently.

**Why?** Lower storage cost, but retrieval charges apply.

[Госфильмофонд  показываем самое большое в мире хранилище киноплёнок из книги рекордов Гиннесса в блоге Своими глазами / Сделано у нас](https://images.openai.com/static-rsc-4/EYAlgCxYHhM5iOy7YmwkBXio-UduT4CyGWYdhNKjGueEMK6o1S-GNdKBNgPjcCK2R60ONZyEMLnB5GVkAr3XEGsjV5zhKhOfgEOxGZUJ5DcM_VllJJwxcTJ_0zm0ISj7ifss1_GyLabCnjzWDr1zXSmZCKbpn_mRJTKDX6VP_OA?purpose=inline)

**S3 One Zone-IA – Re-creatable movie copies**

Example: A secondary copy of an old transcoded movie that can be recreated from a protected master copy.

Stored in one Availability Zone.

**Why?** Lower storage cost, but less resilient to AZ loss.

[9 Best Websites For Public Domain Movies To Watch Right Now](https://images.openai.com/static-rsc-4/42E9AZAv07tlk-vOfMJkjX-EoEfy0mB8XwcU0maxUcMXZN9drSgc0iJmflYc7e9rErCUvoTtcUxzMXQLeEbEaLluinHl8gatnhoLJoDXNw5sNVBZlSyduT9UiXZDJIgDm9p52_IQ4gIOoYRA9nXQA6Ax2zxR1_9M_blR6uogEwU?purpose=inline)

**S3 Glacier Instant Retrieval – Rarely watched classic movies**

Example: Old classic movies that customers might occasionally request.

The data can still be retrieved in milliseconds.

**Why?** Archive storage with instant retrieval.

[US-ENTERTAINMENT-FILM-CINEMA-HISTORY](https://images.openai.com/static-rsc-4/O2g32V_i9LjLLKBRjAzHxYtgcRLPl85_w8NoWehKvUXfvygA_OcJ9IlcgWg8Nl-jh-AGdK8dVH8rV0kb_FmTV610O5xZdw59JW0mWMjGep8Acpq347K5O_QqXxiSlrSBOk2wchQ-aVHpG0nbV6lLJhyPACX1Qgrro_t6r7YoeopSMMVSyqoMgo_7yvY4tf6J?purpose=inline)

**S3 Glacier Flexible Retrieval – Old movie archives**

Example: Old movie masters retained for historical or business purposes.

If the company needs them, it can request restoration and wait minutes to hours.

**Why?** Rarely accessed data with lower storage cost.

[US-ENTERTAINMENT-FILM-CINEMA-HISTORY](https://images.openai.com/static-rsc-4/Bn4PUVvgtPrlGhDW3hT2RDvau8aSXeLe0WwNMc4fw_alRWg2u56P9EeiWuAF-ZYEQDHeOHYhXGsIKrxJASL2V2xhUP0GzT-ygzZ7JnaQI-rfWZZaQTAAiFfs-5Y4SOFiOzzPM0WCzs_3R1T7UfgSsSi_BsKoZ91ybcOYZnHzDpOd88WpTVIyxNJyvUT1PPj9?purpose=inline)

**S3 Glacier Deep Archive – Long-term movie preservation**

Example: Very old movie masters retained for several years for preservation or compliance.

Retrieval can take hours.

**Why?** Very rarely accessed data and very low storage cost.

[Mux vs. Cloudflare Stream | Mux](https://images.openai.com/static-rsc-4/H3tW6cNcTbBbpETRBooW7Yn5nQ2GjnHGXDKsTo4d5p1d7sDO6qmnyEZIOaZZvXFYcC_HTGwRjKQ8Dl7gI0Yakh4VxMAj0uwwzIL5E8i103lvmv2D7U3SR6MKmRkhOy2YE_6suXecwlcTO2p2iHYmNXGFNlVvxnbDoLiqeHARbvs?purpose=inline)

**S3 Intelligent-Tiering – Movies with unpredictable viewing patterns**

Example: A movie suddenly becomes popular because of a social media trend.

AWS automatically moves eligible objects between access tiers based on access patterns.

**Why?** We don't know which movies customers will watch frequently.

These are teaching scenarios, not a claim that Prime Video uses these exact storage classes for its movie catalog. The actual choice depends on access patterns, retrieval requirements and business needs.&#x20;

[image](https://www.google.com/s2/favicons?domain=https://docs.aws.amazon.com\&sz=32)

Amazon Simple Storage Service+2



## **2. Explain using one simple diagram**

[Let’s Architect! Modern data architectures | AWS Architecture Blog](https://images.openai.com/static-rsc-4/ufomW17EKNwHLEaijadwMmWSzRai2jb0gzcSARmYJYUUTwnx6lZI4ygU_ziwKPln0D_gF1ZtaezMLMiVIujXHKs-oxSYOq-AX_UBqZVvY4unAdFrPeqDNBuI9BStrl7j_AvysZ1hKyztecXy4BoTySUw8Mx4gtqE0vVvhYGQP_M?purpose=inline)

[aws.amazon.com](https://aws.amazon.com/blogs/architecture/lets-architect-modern-data-architectures-2/?utm_source=chatgpt.com)

Tell students:

"When a movie is newly released, it may be watched frequently. As time passes, fewer customers may watch it. So we can move its stored data to cheaper storage classes according to its access requirements."

## **3. Prime Video: Example of Lifecycle Policy**

Now explain how a DevOps Engineer can automate this process.

Suppose a movie called **"Super Hero – 2026"** is uploaded to S3.

Here is a hypothetical lifecycle strategy:

## **Movie storage lifecycle**

1. **Day 0 – S3 Standard**

   New movie uploaded. It is expected to receive frequent views.
2. **After 30 days – S3 Standard-IA**

   If viewing requirements allow, move it to less expensive storage.
3. **After 120 days – S3 Glacier Instant Retrieval**

   If it is rarely watched but still needs instant retrieval.
4. **After 365 days – S3 Glacier Flexible Retrieval**

   If it is retained for archival purposes and does not need immediate access.
5. **After several years – S3 Glacier Deep Archive**

   If it must be preserved for long-term purposes and retrieval can take hours.

Illustrative timeline, not an AWS recommendation or actual Prime Video policy. Transitions must meet minimum storage-duration and eligibility requirements.

**Important teaching point:** S3 Lifecycle rules work based on object age, not movie popularity. If you want AWS to react to changing access patterns, explain Intelligent-Tiering instead.

## **4. Important comparison for students**

| Storage class              | Availability Zones | Retrieval                                                      |
| -------------------------- | ------------------ | -------------------------------------------------------------- |
| Standard                   | Multiple AZs       | Milliseconds                                                   |
| Intelligent-Tiering        | Multiple AZs       | Milliseconds in frequent, infrequent and Archive Instant tiers |
| Standard-IA                | Multiple AZs       | Milliseconds                                                   |
| One Zone-IA                | Single AZ          | Milliseconds                                                   |
| Glacier Instant Retrieval  | Multiple AZs       | Milliseconds                                                   |
| Glacier Flexible Retrieval | Multiple AZs       | Minutes to hours                                               |
| Glacier Deep Archive       | Multiple AZs       | Hours                                                          |

[image](https://www.google.com/s2/favicons?domain=https://docs.aws.amazon.com\&sz=32)

Amazon Simple Storage Service+2

## **5. Ask students these questions**

1. A new movie is released and millions of people watch it. Which storage class would you choose?
2. An old movie is watched occasionally but needs immediate retrieval. Which class?
3. A movie master must be retained for 10 years and is rarely accessed. Which class?
4. A movie's access pattern is unpredictable. Which class?
5. Why would you not use Glacier Deep Archive for a movie that customers want to watch immediately?

## **6. One simple way to conclude the lesson**

Tell students:

"Think of S3 Storage Classes like storing movies in a library."

- New and popular movies are kept where they can be accessed frequently.
- Less popular movies are stored in cheaper storage.
- Very old movies are moved to archival storage.
- Movies that must be preserved for many years are kept in long-term archives.

**The main concept is:**

> The less frequently we access data, the cheaper storage options we can consider, provided the retrieval time and availability meet business requirements.

Official reference: [AWS S3 Storage Classes](https://docs.aws.amazon.com/AmazonS3/latest/userguide/storage-class-intro.html?utm_source=chatgpt.com).
