# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-09-12T14:10:01.358788+09:00

### 次に取るべきアクション
> RED最優先: CIRCUIT_BREAKER_TRIP×61 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×68 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×61 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🔴 CALIBRATION_DRIFT×5 (24h)
- 🟡 LARGE_ODDS_DRIFT×2 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 CIRCUIT_BREAKER_TRIP  ×15  [2026-09-12T14:05:35]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×15  [2026-09-12T14:05:35]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 STRATEGY_CI_FAIL  ×5  [2026-09-12T14:05:35]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🟡 KS_ODDS_DRIFT  ×5  [2026-09-12T14:05:35]
- key: `KS_ODDS_DRIFT|`
- **FIX**: オッズ分布の KS 検定 p<0.01→市場構造変化の可能性。settlement_ratio の fallback 値を再検証

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×9  [2026-09-12T13:31:38]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×3  [2026-09-12T13:00:04]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S00 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×3  [2026-09-12T13:00:04]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S01_NAKAANA1 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×3  [2026-09-12T13:00:04]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S02_TETSUBAN が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×25  [2026-09-12T11:58:35]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### 🔴 CALIBRATION_DRIFT  ×8  [2026-09-12T11:27:20]
- key: `CALIBRATION_DRIFT|`
- **FIX**: 予測確率が実的中率から50%以上乖離→isotonic_calibration.json 再生成 or モデル再学習が必要。EV計算が膨張中

### 🟡 ANOMALY_BET_VOLUME_DROP  ×56  [2026-09-12T10:00:37]
- key: `ANOMALY_BET_VOLUME_DROP|`
- **FIX**: 本日のbet数が7日baselineから2σ低下。戦略filter/ scan fix/run_cycle停止を疑え

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-09-12T06:00:29]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=84<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-09-12T06:00:29]
- key: `INSUFFICIENT_SAMPLE|S00: n=179<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-09-12T06:00:29]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=185<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ CALIBRATION_LIVE  ×1  [2026-09-12T06:00:29]
- key: `CALIBRATION_LIVE|decile 0.15-0.20: n=9 pred=0.1773 actual=0.2222 gap=-0.0449`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-09-12T06:00:29]
- key: `CALIBRATION_LIVE|decile 0.30-0.40: n=46 pred=0.3225 actual=0.3043 gap=+0.0182`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-09-12T06:00:29]
- key: `CALIBRATION_LIVE|decile 0.10-0.15: n=6 pred=0.1314 actual=0.0000 gap=+0.1314`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-09-12T06:00:29]
- key: `DRIFT_BUCKET|drift -10%〜+10%: n=98 hit%=23.5% ROI=0.88 (コスト 22,600/回収 19,910)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ CALIBRATION_LIVE  ×1  [2026-09-12T06:00:29]
- key: `CALIBRATION_LIVE|decile 0.20-0.30: n=8 pred=0.2235 actual=0.1250 gap=+0.0985`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-09-12T06:00:29]
- key: `ROI_STAT|S00: n=179 hit%=27.4% hit_CI[Bonf]=[18.9,37.8]% ROI=0.92 ROI_boot95=[0.65,1.24]`
- **FIX**: 統計サマリ情報。判定ではなく参照用


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 13.04MB / last modified 2026-09-12T14:09:57.489804+09:00

### データファイル存在確認
| file | exists | md5 | size |
|---|---|---|---|
| lgbm_model_top1.txt | True | `5b55d55bdb59df95ccfd1745d4e9b469` | 769682 |
| lgbm_model_top3.txt | True | `d5fd8d8393fd859ed913813abbf60084` | 969111 |
| calibration_v7.json | True | `1c04ab3c1a1f074da889e6f5f06adbf3` | 1450 |
| pl_corr_v8_final.json | True | `8727224dfcc3d7548845e2e41caef7be` | 1209 |

### crontab
```
# boatrace_v2 - managed by めう/Claude
SHELL=/bin/bash
PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin

# 1分毎: 統合サイクル (run_cycle.py, flock で並行実行防止)
* 8-23 * * * cd /opt/boatrace_v2 && flock -n /var/lock/run_cycle.lock /opt/boatrace/venv/bin/python3 run_cycle.py >> logs/run_cycle.log 2>&1

# 10分毎: pending alert flush
*/10 * * * * cd /opt/boatrace_v2 && /opt/boatrace/venv/bin/python3 dispatch_pending.py >> logs/dispatch.log 2>&1

# 10分毎: snapshot 生成 + GitHub 同期 (Claude 次セッション用)
*/10 * * * * cd /opt/boatrace_v2 && bash sync_snapshot_to_github.sh >> logs/sync_snapshot.log 2>&1

# 5分毎: 結果取得
*/5 * * * * cd /opt/boatrace_v2 && /opt/boatrace/venv/bin/python3 record_results.py >> logs/results.log 2>&1

# 30分毎: health check
*/30 * * * * cd /opt/boatrace_v2 && /opt/boatrace/venv/bin/python3 health.py >> logs/health.log 2>&1

# 6時: 日次総合検査
0 6 * * *  cd /opt/boatrace_v2 && /opt/boatrace/venv/bin/python3 verify_all.py >> logs/verify_all.log 2>&1

# 0時: 日次集計
5 0 * * *  cd /opt/boatrace_v2 && /opt/boatrace/venv/bin/python3 daily_summary.py >> logs/daily.log 2>&1
0 3 * * * find /opt -maxdepth 1 -name "boatrace_v2.bak_*" -mtime +7 -exec rm -rf {} \; # backup cleanup

# 30分毎: コード/DB a
```

### 直近 run_cycle ログ (末尾)
```
d=20260912: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 3s
2026-09-12 14:09:39,954 [INFO] scraper: odds3t: 120/120 parsed
2026-09-12 14:09:41,043 [INFO] scraper: odds3f: 20/20 parsed
2026-09-12 14:09:42,152 [INFO] scraper: odds2t: 30/30 parsed
2026-09-12 14:09:42,154 [INFO] scraper: odds2f: 15/15 parsed
2026-09-12 14:09:43,238 [INFO] scraper: odds_win: 6/6 parsed
2026-09-12 14:09:43,239 [INFO] scraper: fetch_race 10/12: boats=6 odds=191/191
2026-09-12 14:09:43,243 [INFO] predictor: CALIBRATION_MODE=on
2026-09-12 14:09:43,243 [INFO] predictor: combos: {'win': 6, '2t': 30, '3t': 120}
2026-09-12 14:09:43,248 [INFO] run_cycle: fetched 10/12 [final]: 156 combos
2026-09-12 14:09:46,922 [INFO] scraper: odds3t: 120/120 parsed
2026-09-12 14:09:48,015 [INFO] scraper: odds3f: 20/20 parsed
2026-09-12 14:09:49,170 [INFO] scraper: odds2t: 30/30 parsed
2026-09-12 14:09:49,171 [INFO] scraper: odds2f: 15/15 parsed
2026-09-12 14:09:50,262 [INFO] scraper: odds_win: 5/6 parsed
2026-09-12 14:09:50,262 [INFO] scraper: fetch_race 02/8: boats=6 odds=190/191
2026-09-12 14:09:50,265 [INFO] predictor: CALIBRATION_MODE=on
2026-09-12 14:09:50,265 [INFO] predictor: combos: {'win': 5, '2t': 30, '3t': 120}
2026-09-12 14:09:50,269 [INFO] run_cycle: fetched 02/8 [scan]: 155 combos
2026-09-12 14:09:53,753 [INFO] scraper: odds3t: 120/120 parsed
2026-09-12 14:09:54,909 [INFO] scraper: odds3f: 20/20 parsed
2026-09-12 14:09:55,991 [INFO] scraper: odds2t: 30/30 parsed
2026-09-12 14:09:55,992 [INFO] scraper: odds2f: 15/15 parsed
2026-09-12 14:09:57,152 [INFO] scraper: odds_win: 6/6 parsed
2026-09-12 14:09:57,152 [INFO] scraper: fetch_race 18/8: boats=6 odds=191/191
2026-09-12 14:09:57,155 [INFO] predictor: CALIBRATION_MODE=on
2026-09-12 14:09:57,155 [INFO] predictor: combos: {'win': 6, '2t': 30, '3t': 120}
2026-09-12 14:09:57,159 [INFO] run_cycle: fetched 18/8 [scan]: 156 combos
2026-09-12 14:09:57,275 [INFO] run_cycle: run_cycle done: 0 notifications

```

## 戦略有効/無効一覧
| id | trust | bt | ev_th | pmin | enabled |
|---|---|---|---|---|---|
| S00 | S | win | 4.0 | 0.0 | True |
| S01_NAKAANA1 | A | win | 1.5 | 0.0 | True |
| S02_TETSUBAN | A | win | 1.0 | 0.0 | True |
| S03_NAKAANA4 | B | win | 1.0 | 0.0 | False |
| S04_SELL_3T | B | 3t | 1.0 | 0.0 | False |
| S05_2T_MANKEN | B | 2t | 1.0 | 0.0 | False |
| S06_2F_AXIS1 | B | 2f | 1.0 | 0.0 | False |
| S07_2T_HONMEI | B | 2t | 1.0 | 0.0 | False |

## Webhook送信 (24h)
```
[
  {
    "target": "mirror",
    "ok": 1,
    "c": 45
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 45
  }
]
```

## Phase別通知記録 (24h)
{'final': 17, 'result': 7, 'scan': 21}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 178
  FINAL_MISSING: 68
  CIRCUIT_BREAKER_TRIP: 61
  CIRCUIT_BREAKER_NO_ACTION: 51
  KS_ODDS_DRIFT: 35
  ANOMALY_SCAN_FINAL_RATIO: 18
  STRATEGY_CI_FAIL: 17
  ANOMALY_BET_VOLUME_DROP: 12
  CALIBRATION_DRIFT: 5
  LARGE_ODDS_DRIFT: 2
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 29 | 6 | 8,700 | 5,280 | -3,420 | 0.607 |
| S01_NAKAANA1 | 38 | 8 | 7,600 | 5,220 | -2,380 | 0.687 |
| S02_TETSUBAN | 22 | 8 | 4,400 | 2,400 | -2,000 | 0.545 |

## 直近アラート (24h・新しい順)
```
[14:03:34] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[14:03:34] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S02_TETSUBAN"}
[14:03:34] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S01_NAKAANA1"}
[14:03:34] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S00"}
[13:59:25] CIRCUIT_BREAKER_TRIP: {"cost": 8700, "kind": "CIRCUIT_BREAKER_TRIP", "n": 29, "payout": 5280, "roi_7d": 0.607, "sid": "S00"}
[13:54:34] KS_ODDS_DRIFT: {"kind": "KS_ODDS_DRIFT", "ks_p": 0.003203, "ks_stat": 0.211}
[13:49:21] FINAL_MISSING: {"deadline": "2026-09-12T10:18:00+09:00", "kind": "FINAL_MISSING", "nid": "2026091210051018", "sid": "S00"}
[13:44:05] FINAL_MISSING: {"deadline": "2026-09-12T13:14:00+09:00", "kind": "FINAL_MISSING", "nid": "2026091202061314", "sid": "S00"}
[13:40:23] KS_ODDS_DRIFT: {"kind": "KS_ODDS_DRIFT", "ks_p": 0.002858, "ks_stat": 0.212}
[13:36:29] CIRCUIT_BREAKER_TRIP: {"cost": 4400, "kind": "CIRCUIT_BREAKER_TRIP", "n": 22, "payout": 2400, "roi_7d": 0.545, "sid": "S02_TETSUBAN"}
```

## 本日残レース: 77件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 156件 登録 / 79件 締切済
- 通知発射: scan=14 nid / final=10 nid / result=4 nid
- predictions: 4 / うち結果DB記録済: 4
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 5件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S00 | 024R | win | 1 | 0.4111 | 8.3 | 3.41 | 300 | scan=6.2 drift=+33.9% | 12:11:31 |
| S01_NAKAANA1 | 023R | win | 1 | 0.4111 | 3.0 | 1.23 | 200 | scan=3.8 drift=-21.1% | 11:42:54 |
| S00 | 022R | win | 1 | 0.4111 | 5.6 | 2.30 | 300 | scan=4.1 drift=+36.6% | 11:13:26 |
| S00 | 216R | win | 1 | 0.5719 | 4.3 | 2.46 | 300 | scan=- drift=- | 10:56:32 |
| S01_NAKAANA1 | 204R | win | 1 | 0.5334 | 3.0 | 1.60 | 200 | scan=- drift=- | 16:38:21 |
| S01_NAKAANA1 | 201R | win | 1 | 0.4111 | 3.3 | 1.36 | 200 | scan=3.7 drift=-10.8% | 15:20:51 |
| S01_NAKAANA1 | 066R | win | 1 | 0.5086 | 3.1 | 1.58 | 200 | scan=- drift=- | 13:51:32 |
| S01_NAKAANA1 | 055R | win | 1 | 0.4111 | 3.4 | 1.40 | 200 | scan=3.7 drift=-8.1% | 12:58:22 |
| S02_TETSUBAN | 051R | win | 1 | 0.5735 | 2.2 | 1.26 | 200 | scan=2.2 drift=+0.0% | 11:00:30 |
| S02_TETSUBAN | 2010R | win | 1 | 0.5123 | 2.1 | 1.08 | 200 | scan=2.2 drift=-4.5% | 19:22:20 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 51 | +6.0% | -49.1% | +137.8% | 18 | 7 | 33 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 535.3s |
| **Latency** (scan→final max) | 625.1s |
| **Traffic** (notifications 24h) | 45 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 900円 used |
| **Saturation** (S01_NAKAANA1) | 200円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 445 | 0.4702 | 0.2652 | +0.2050 | 🟡+44% | 0.2395 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 178 | 0.4245 | 0.2697 | 0.2176 | 🔴-0.10 | 0.917 |
| S01_NAKAANA1 | win | 183 | 0.4803 | 0.2350 | 0.2474 | 🔴-0.38 | 0.745 |
| S02_TETSUBAN | win | 84 | 0.5449 | 0.3214 | 0.2686 | 🔴-0.23 | 0.563 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.10-0.15 | 6 | 0.1314 | 0.0000 | 🔴+0.1314 |
| 0.15-0.20 | 8 | 0.1750 | 0.2500 | 🔴-0.0750 |
| 0.20-0.30 | 8 | 0.2235 | 0.1250 | 🔴+0.0985 |
| 0.30-0.50 | 163 | 0.4016 | 0.2209 | 🔴+0.1808 |
| 0.50+ | 256 | 0.5449 | 0.3047 | 🔴+0.2402 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 135 | 0.768 |
| win | <5.0 | ✅learned | 242 | 0.748 |
| win | <10.0 | ✅learned | 120 | 0.468 |
| win | <20.0 | ✅learned | 31 | 0.231 |
| win | <50.0 | ⚠️fallback | 8 | 0.1 |
| win | ∞ | ⚠️fallback | 0 | 0.1 |
| 2t | <10.0 | ⚠️fallback | 0 | 0.5 |
| 2t | <30.0 | ⚠️fallback | 0 | 0.35 |
| 2t | ∞ | ⚠️fallback | 0 | 0.25 |
| 3t | <10.0 | ⚠️fallback | 1 | 0.4 |
| 3t | <50.0 | ⚠️fallback | 0 | 0.4 |
| 3t | <200.0 | ⚠️fallback | 0 | 0.3 |
| 3t | ∞ | ⚠️fallback | 0 | 0.2 |
| 2f | <10.0 | ⚠️fallback | 0 | 0.45 |
| 2f | ∞ | ⚠️fallback | 0 | 0.3 |
| 3f | <50.0 | ⚠️fallback | 0 | 0.4 |
| 3f | ∞ | ⚠️fallback | 0 | 0.25 |

---
_auto-generated by claude_snapshot.py at 2026-09-12T14:10:01.358788+09:00_