import pandas as pd #pandas kütüphanemizi import ediyoruz.
df=pd.read_csv("2.hafta/persona.csv") #csv dosyamızı df atamasını yapıyoruz.
df.head()


df=pd.read_csv("persona.csv")
df.head()

df.nunique()   #df içindeki eşssiz(unique) değer sayısını ve frekanslarını verir

df["SOURCE"].nunique()  #SOURCE değişkeni özelinde kaç farklı değer olduğunu gösterir.
df["SOURCE"].value_counts() # frekansını gösterir.


df.nunique()

df["PRICE"].nunique()
df["PRICE"].value_counts()

df["COUNTRY"].value_counts()

       # ya da
       
df.groupby("COUNTRY")["PRICE"].count()



df.groupby("COUNTRY")["PRICE"].sum()


df.groupby("SOURCE")["PRICE"].count()


df.groupby('SOURCE').agg({'PRICE': 'sum'})


df.groupby("COUNTRY")["PRICE"].aggregate("mean")



df.groupby("SOURCE")["PRICE"].aggregate("mean")


df.groupby(["COUNTRY", "SOURCE"])["PRICE"].aggregate("mean")




df.groupby('SOURCE').agg({'PRICE': 'mean'})


df.groupby(["COUNTRY", "SOURCE", "SEX", "AGE"])["PRICE"].aggregate("mean")


df.groupby(["COUNTRY", "SOURCE", "SEX", "AGE"])["PRICE"].aggregate("mean")


agg_df = df.sort_values(by=['PRICE'], ascending=True)





df.groupby("COUNTRY")["PRICE"].aggregate("mean")


df.groupby(["COUNTRY", "SOURCE", "SEX", "AGE"])["PRICE"].aggregate("mean")


df.groupby("SOURCE")["PRICE"].aggregate("mean")
df.groupby(["COUNTRY", "SOURCE"])["PRICE"].aggregate("mean")
df.groupby(["COUNTRY", "SOURCE", "SEX", "AGE"])["PRICE"].aggregate("mean")
df.groupby(["COUNTRY", "SOURCE", "SEX", "AGE"])["PRICE"].aggregate("mean")
agg_df = df.sort_values(by=['PRICE'], ascending=True)



agg_df = df.groupby(["COUNTRY","SOURCE","SEX","AGE"], as_index=False).PRICE.mean().head()
agg_df = df.groupby(by=["COUNTRY", 'SOURCE', "SEX", "AGE"]).agg({"PRICE": "mean"}).sort_values("PRICE", ascending=False)
agg_df


agg_df = agg_df.reset_index()
agg_df.head()



# AGE değişkeninin bölümleri
bins = [0, 18, 23, 30, 40, agg_df["AGE"].max()]


# Bölünen noktalara karşılık isimlendirmelerin ne olacağını ifade edelim:
mylabels = ['0_18', '19_23', '24_30', '31_40', '41_' + str(agg_df["AGE"].max())]

#age'i bölelim:
agg_df["age_cat"] = pd.cut(agg_df["AGE"], bins, labels=mylabels)
agg_df.head()

# değişken isimleri:
agg_df.columns
#####################################


agg_df["customers_level_based"] = [row[0].upper() + "_" + row[1].upper() + "_" + row[2].upper() + "_" + row[5].upper() for row in agg_df.values]
agg_df.head()


# Gereksiz değişkenleri çıkaralım:
agg_df = agg_df[["customers_level_based", "PRICE"]]
agg_df.head()
agg_df["customers_level_based"].value_counts()


agg_df = agg_df.groupby("customers_level_based").agg({"PRICE": "mean"})
agg_df = agg_df.reset_index()
agg_df.head()

agg_df["customers_level_based"].value_counts()
agg_df.head()

