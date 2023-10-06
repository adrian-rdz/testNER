from fastapi import FastAPI,Request
import uvicorn
import spacy

#Cargar modelo NLP
nlp = spacy.load('es_core_news_sm')


def process_json_oraciones(request):
    dict_res= {}
    dict_res['resultados'] = []
    for i,x in enumerate(request['oraciones']):
        # print(i,x)
        doc = nlp(x)
        dict_res['resultados'].append({})
        dict_res['resultados'][i]['oracion']=x
        dict_res['resultados'][i]['entidades'] ={entity.text:entity.label_  for entity in doc.ents}
    return dict_res


app = FastAPI()

@app.post('/ner/')
async def get_body(request: Request):
        req = await request.json()
        output = process_json_oraciones(req)
        return output

