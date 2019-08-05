# Amharic-Simple-Text-Preprocessing-Usin-Python
# Short Form Expansion and Character Level Normalization 
<pre>
import re
class normalize(object):
    expansion_file_dir='' # assume you have file with list of short forms with their expansion as gazeter
    short_form_dict={}
    # Constructor
    def __init__(self):
       self.short_form_dict=self.get_short_forms()
        

    def get_short_forms(self):
         text=open(self.expansion_file_dir,encoding='utf8')
         exp={}
         for line in iter(text):
            line=line.strip()
            if not line:  # line is blank
                continue
            else:
                expanded=line.split("-")
                exp[expanded[0].strip()]=expanded[1].replace(" ",'_').strip()
         return exp
                     

    # method that expand short form file
    def expand_short_form(self,input_short_word):
        if input_short_word in self.short_form_dict:              
            return self.short_form_dict[input_short_word]
        else:
            return input_short_word

        #method to normalize character level missmatch such as ጸሀይ and ፀሐይ
    def normalize_char_level_missmatch(self,input_token):
        rep1=re.sub('[ሃኅኃሐሓኻ]','ሀ',input_token)
        rep2=re.sub('[ሑኁዅ]','ሁ',rep1)
        rep3=re.sub('[ኂሒኺ]','ሂ',rep2)
        rep4=re.sub('[ኌሔዄ]','ሄ',rep3)
        rep5=re.sub('[ሕኅ]','ህ',rep4)
        rep6=re.sub('[ኆሖኾ]','ሆ',rep5)
        rep7=re.sub('[ሠ]','ሰ',rep6)
        rep8=re.sub('[ሡ]','ሱ',rep7)
        rep9=re.sub('[ሢ]','ሲ',rep8)
        rep10=re.sub('[ሣ]','ሳ',rep9)
        rep11=re.sub('[ሤ]','ሴ',rep10)
        rep12=re.sub('[ሥ]','ስ',rep11)
        rep13=re.sub('[ሦ]','ሶ',rep12)
        rep14=re.sub('[ዓኣዐ]','አ',rep13)
        rep15=re.sub('[ዑ]','ኡ',rep14)
        rep16=re.sub('[ዒ]','ኢ',rep15)
        rep17=re.sub('[ዔ]','ኤ',rep16)
        rep18=re.sub('[ዕ]','እ',rep17)
        rep19=re.sub('[ዖ]','ኦ',rep18)
        rep20=re.sub('[ጸ]','ፀ',rep19)
        rep21=re.sub('[ጹ]','ፁ',rep20)
        rep22=re.sub('[ጺ]','ፂ',rep21)
        rep23=re.sub('[ጻ]','ፃ',rep22)
        rep24=re.sub('[ጼ]','ፄ',rep23)
        rep25=re.sub('[ጽ]','ፅ',rep24)
        rep26=re.sub('[ጾ]','ፆ',rep25)
        #Normalizing words with Labialized Amharic characters such as በልቱዋል or  በልቱአል to  በልቷል  
        rep27=re.sub('(ሉ[ዋአ])','ሏ',rep26)
        rep28=re.sub('(ሙ[ዋአ])','ሟ',rep27)
        rep29=re.sub('(ቱ[ዋአ])','ቷ',rep28)
        rep30=re.sub('(ሩ[ዋአ])','ሯ',rep29)
        rep31=re.sub('(ሱ[ዋአ])','ሷ',rep30)
        rep32=re.sub('(ሹ[ዋአ])','ሿ',rep31)
        rep33=re.sub('(ቁ[ዋአ])','ቋ',rep32)
        rep34=re.sub('(ቡ[ዋአ])','ቧ',rep33)
        rep35=re.sub('(ቹ[ዋአ])','ቿ',rep34)
        rep36=re.sub('(ሁ[ዋአ])','ኋ',rep35)
        rep37=re.sub('(ኑ[ዋአ])','ኗ',rep36)
        rep38=re.sub('(ኙ[ዋአ])','ኟ',rep37)
        rep39=re.sub('(ኩ[ዋአ])','ኳ',rep38)
        rep40=re.sub('(ዙ[ዋአ])','ዟ',rep39)
        rep41=re.sub('(ጉ[ዋአ])','ጓ',rep40)
        rep42=re.sub('(ደ[ዋአ])','ዷ',rep41)
        rep43=re.sub('(ጡ[ዋአ])','ጧ',rep42)
        rep44=re.sub('(ጩ[ዋአ])','ጯ',rep43)
        rep45=re.sub('(ጹ[ዋአ])','ጿ',rep44)
        rep46=re.sub('(ፉ[ዋአ])','ፏ',rep45)
        rep47=re.sub('[ቊ]','ቁ',rep46) #ቁ can be written as ቊ
        rep48=re.sub('[ኵ]','ኩ',rep47) #ኩ can be also written as ኵ  
        
        return rep48
    
     #replacing any existance of special character or punctuation to null  
    def remove_punc_and_special_chars(self,sentence_input): # puct in amh =፡።፤;፦፧፨፠፣ 
        normalized_text = re.sub('[\!\@\#\$\%\^\«\»\&\*\(\)\…\[\]\{\}\;\“\”\›\’\‘\"\'\:\,\.\‹\/\<\>\?\\\\|\`\´\~\-\=\+\፡\።\፤\;\፦\፥\፧\፨\፠\፣]', '',sentence_input) 
        return normalized_text
    
    #remove all ascii characters and Arabic and Amharic numbers
    def remove_ascii_and_numbers(self,text_input):
        rm_num_and_ascii=re.sub('[A-Za-z0-9]','',text_input)
        return re.sub('[\'\u1369-\u137C\']+','',rm_num_and_ascii)


</pre>

# A little bit extended version
<pre>

class DirConfig(object):
    BASE_DIR = '../'
    DATA_DIR = BASE_DIR+'Dataset/'
    MODEL_DIR='Models/'
    EMBED_DIR=MODEL_DIR+'Embedding/'
    PREPROCESSED_DIR=DATA_DIR +'normalized/' 
from nltk import BigramCollocationFinder
import nltk.collocations 
import io
import re
import os
class normalize(object):
    def tokenize(self,corpus):
        print('Tokenization ...')
        all_tokens=[]
        for sentence in corpus:
            tokens=re.compile('[\s+]+').split(sentence)
            all_tokens.extend(tokens)
        
        return all_tokens

    def get_short_forms(self,_file_dir):
        
         text=open(_file_dir,encoding='utf8')
         exp={}
         for line in iter(text):
            line=line.strip()
            if not line:  # line is blank
                continue
            else:
                expanded=line.split("-")
                exp[expanded[0].strip()]=expanded[1].replace(" ",'_').strip()
         return exp
                
    def collocation_finder(self,tokens,bigram_dir):
   
        bigram_measures = nltk.collocations.BigramAssocMeasures()
        
        #Search for bigrams with in a corpus
        finder = BigramCollocationFinder.from_words(tokens)
        
        #filter only Ngram appears morethan 3+ times
        finder.apply_freq_filter(3)
        
        frequent_bigrams = finder.nbest(bigram_measures.chi_sq,5) # chi square computer 
        print(frequent_bigrams)
        PhraseWriter = io.open(bigram_dir, "w", encoding="utf8")
        
        for bigram in frequent_bigrams:
            PhraseWriter.write(bigram[0]+' '+bigram[1] + "\n")
   
    def normalize_multi_words(self,tokenized_sentence,bigram_dir,corpus):
      
        bigram=set()
        sent_with_bigrams=[]
        index=0
        if not os.path.exists(bigram_dir):
            self.collocation_finder(self.tokenize(corpus),bigram_dir)
            #calling itsef
            self.normalize_multi_words(tokenized_sentence,bigram_dir,corpus)
        else:
            text=open(bigram_dir,encoding='utf8')
           
            for line in iter(text):
               line=line.strip()
               if not line:  # line is blank
                   continue
               else:
                   bigram.add(line)
            if len(tokenized_sentence)==1:
                sent_with_bigrams=tokenized_sentence
            else:
                while index <=len(tokenized_sentence)-2:
                    mword=tokenized_sentence[index]+' '+tokenized_sentence[index+1]
                    if mword in bigram:
                        sent_with_bigrams.append(tokenized_sentence[index]+''+tokenized_sentence[index+1])
                        index+=1
                    else:
                        sent_with_bigrams.append(tokenized_sentence[index])
                    index+=1
                    if index==len(tokenized_sentence)-1:
                        sent_with_bigrams.append(tokenized_sentence[index])
                
            return sent_with_bigrams
    # method that expand short form file
    def expand_short_form(self,input_short_word,_file_dir):
       
        if not os.path.exists(_file_dir):
            return input_short_word
        else:
            short_form_dict=self.get_short_forms(_file_dir)
            if input_short_word in short_form_dict:              
                return short_form_dict[input_short_word]
            else:
                return input_short_word

        #method to normalize character level missmatch such as ጸሀይ and ፀሐይ
    def normalize_char_level_missmatch(self,input_token,lang_resource):
       
         if not os.path.exists(lang_resource):
            return input_token
         else:
            text=open(lang_resource,encoding='utf8')
            rep=input_token
            for line in iter(text):
               line=line.strip()
               if not line:  # line is blank
                   continue
               else:
                   chars=line.split()
                   chars_from=chars[0]
                   chars_to=chars[1]
                   rep=re.sub('['+chars_from+']',chars_to,rep)
            return rep
    
     #replacing any existance of special character or punctuation to null  
    def remove_punc_and_special_chars(self,sentence_input,lang_resource): # puct in amh =፡።፤;፦፧፨፠፣ 
        if not os.path.exists(lang_resource):
            return sentence_input
        else:
            text=open(lang_resource,encoding='utf8')
            chars=text.read()
            sp_chars=chars.split(' ')
            punct=set(sp_chars)
            normalized_text=sentence_input
            for p in punct:
                normalized_text = re.sub('[\\'+p+']', '',normalized_text) 
            return normalized_text   
    
    def preprocess_text(self,text_input,model_dir,corpus):
        normalzed_text=[]
        CHARS_DIR=model_dir+DirConfig.CHARS_DIR
        MULTI_DIR=model_dir+DirConfig.MULTI_DIR
        ABRV_DIR=model_dir+DirConfig.ABRV_DIR
        PUNCT_DIR=model_dir+DirConfig.PUNCT_DIR
        print('Preprocessing '+str(len(text_input))+' sentences ....')
        for sentence in text_input:
            tokens=re.compile('[\s+]+').split(sentence)
            normalized_token=[]
            multi_words=self.normalize_multi_words(tokens,MULTI_DIR, corpus)         
            for token in tokens:
                short_rem=self.expand_short_form(token,ABRV_DIR)
                char_normalized=self.normalize_char_level_missmatch(short_rem,CHARS_DIR)
                punct_rem=self.remove_punc_and_special_chars(char_normalized,PUNCT_DIR)
                normalized_token.append(punct_rem)
                normalized_token.append(token)
            normalzed_text.append(normalized_token)
        
        return normalzed_text
</pre>

# Normalize Geez and Arabic Number Mismatch
This code snippet allows you to expand decimal form numbers to text representation. It also automatically normalize arabic numbers to Geez form.

<pre>
def arabic2geez(arabicNumber):
        ETHIOPIC_ONE= 0x1369
        ETHIOPIC_TEN= 0x1372
        ETHIOPIC_HUNDRED= 0x137B
        ETHIOPIC_TEN_THOUSAND = 0x137C
        arabicNumber=str(arabicNumber)
        n = len(arabicNumber)-1 #length of arabic number
        if n%2 == 0:
            arabicNumber = "0" + arabicNumber
            n+=1
        arabicBigrams=[arabicNumber[i:i+2] for i in range(0,n,2)] #spliting bigrams
        reversedArabic=arabicBigrams[::-1] #reversing list content
        geez=[]
        for index,pair in enumerate(reversedArabic):
            curr_geez=''
            artens=pair[0]#arrabic tens
            arones=pair[1]#arrabic ones
            amtens=''
            amones=''
            if artens!='0':
                amtens=str(chr((int(artens) + (ETHIOPIC_TEN - 1)))) #replacing with Geez 10s [፲,፳,፴, ...]
            else:
                if arones=='0': #for 00 cases
                    continue
            if arones!='0':       
                    amones=str(chr((int(arones) + (ETHIOPIC_ONE - 1)))) #replacing with Geez Ones [፩,፪,፫, ...]
            if index>0:
                if index%2!= 0: #odd index
                    curr_geez=amtens+amones+ str(chr(ETHIOPIC_HUNDRED)) #appending ፻
                else: #even index
                    curr_geez=amtens+amones+ str(chr(ETHIOPIC_TEN_THOUSAND)) # appending ፼
            else: #last bigram (right most part)
                curr_geez=amtens+amones
            
            geez.append(curr_geez)
        
        geez=''.join(geez[::-1])
        if geez.startswith('፩፻') or geez.startswith('፩፼'):
            geez=geez[1:]
        
        if len(arabicNumber)>=7:
            end_zeros=''.join(re.findall('([0]+)$',arabicNumber)[0:])
            i=int(len(end_zeros)/3)
            if len(end_zeros)>=(3*i):
                if i>=3:
                    i-=1
                for thoushand in range(i-1):
                    print(thoushand)                
                    geez+='፼'

        return geez
    def getExpandedNumber(self,number):
        if '.' not in str(number):
            return arabic2geez(number)
        else:
            num,decimal=str(number).split('.')
            if decimal.startswith('0'):
                decimal=decimal[1:]
                dot=' ነጥብ ዜሮ '
            else:
                dot=' ነጥብ '
            return arabic2geez(num)+dot+self.arabic2geez(decimal)

</pre>
