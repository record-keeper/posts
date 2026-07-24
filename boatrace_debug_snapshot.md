# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-07-24T17:10:01.439576+09:00

### 次に取るべきアクション
> RED最優先: CIRCUIT_BREAKER_TRIP×38 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×99 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×38 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🟡 LARGE_ODDS_DRIFT×2 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×8  [2026-07-24T17:06:32]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 STRATEGY_CI_FAIL  ×4  [2026-07-24T17:06:32]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×1  [2026-07-24T17:00:02]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S00 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×1  [2026-07-24T17:00:02]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S01_NAKAANA1 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×11  [2026-07-24T14:01:19]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### 🔴 CIRCUIT_BREAKER_TRIP  ×73  [2026-07-24T13:03:44]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🟡 ANOMALY_BET_VOLUME_SPIKE  ×18  [2026-07-24T11:42:27]
- key: `ANOMALY_BET_VOLUME_SPIKE|`
- **FIX**: 本日のbet数が2σ急増。filter logic緩み・戦略追加・race_schedule異常

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×10  [2026-07-24T10:46:21]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-07-24T06:00:16]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=74<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-07-24T06:00:16]
- key: `INSUFFICIENT_SAMPLE|S00: n=178<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### 🟡 ORPHAN_SCAN  ×1  [2026-07-24T06:00:16]
- key: `ORPHAN_SCAN|172 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-07-24T06:00:16]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=162<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ CALIBRATION_LIVE  ×1  [2026-07-24T06:00:16]
- key: `CALIBRATION_LIVE|decile 0.30-0.40: n=32 pred=0.3249 actual=0.0938 gap=+0.2311`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-07-24T06:00:16]
- key: `ROI_STAT|S00: n=178 hit%=27.5% hit_CI[Bonf]=[19.0,38.0]% ROI=0.73 ROI_boot95=[0.53,0.95]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-07-24T06:00:16]
- key: `ROI_STAT|S01_NAKAANA1: n=162 hit%=28.4% hit_CI[Bonf]=[19.4,39.5]% ROI=0.78 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-07-24T06:00:16]
- key: `ROI_STAT|S02_TETSUBAN: n=74 hit%=48.6% hit_CI[Bonf]=[32.9,64.7]% ROI=0.97 ROI_boot95=[0.7`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-07-24T06:00:16]
- key: `DRIFT_BUCKET|drift ≤-30%: n=33 hit%=27.3% ROI=0.57 (コスト 9,700/回収 5,520)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-07-24T06:00:16]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=44 hit%=31.8% ROI=0.88 (コスト 10,700/回収 9,390)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-07-24T06:00:16]
- key: `DRIFT_BUCKET|drift -10%〜+10%: n=79 hit%=35.4% ROI=0.85 (コスト 18,000/回収 15,350)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-07-24T06:00:16]
- key: `DRIFT_BUCKET|drift +10%〜+30%: n=32 hit%=25.0% ROI=0.50 (コスト 7,700/回収 3,840)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 8.62MB / last modified 2026-07-24T17:09:19.061213+09:00

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
arsed
2026-07-24 17:07:25,037 [INFO] scraper: odds2t: 30/30 parsed
2026-07-24 17:07:25,038 [INFO] scraper: odds2f: 15/15 parsed
2026-07-24 17:07:26,161 [INFO] scraper: odds_win: 6/6 parsed
2026-07-24 17:07:26,161 [INFO] scraper: fetch_race 19/4: boats=6 odds=191/191
2026-07-24 17:07:26,163 [INFO] predictor: CALIBRATION_MODE=on
2026-07-24 17:07:26,163 [INFO] predictor: combos: {'win': 6, '2t': 30, '3t': 120}
2026-07-24 17:07:26,167 [INFO] run_cycle: fetched 19/4 [scan]: 156 combos
2026-07-24 17:07:26,265 [INFO] run_cycle: run_cycle done: 0 notifications
2026-07-24 17:08:03,293 [INFO] run_cycle: === run_cycle 17:08:03 ===
2026-07-24 17:08:03,293 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-07-24 17:08:03,293 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-07-24 17:08:03,337 [INFO] predictor: Models loaded OK
2026-07-24 17:08:03,435 [INFO] run_cycle: run_cycle done: 0 notifications
2026-07-24 17:09:03,208 [INFO] run_cycle: === run_cycle 17:09:03 ===
2026-07-24 17:09:03,208 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-07-24 17:09:03,208 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-07-24 17:09:03,255 [INFO] predictor: Models loaded OK
2026-07-24 17:09:15,642 [INFO] scraper: odds3t: 120/120 parsed
2026-07-24 17:09:16,758 [INFO] scraper: odds3f: 20/20 parsed
2026-07-24 17:09:17,828 [INFO] scraper: odds2t: 30/30 parsed
2026-07-24 17:09:17,829 [INFO] scraper: odds2f: 15/15 parsed
2026-07-24 17:09:18,899 [INFO] scraper: odds_win: 6/6 parsed
2026-07-24 17:09:18,899 [INFO] scraper: fetch_race 22/11: boats=6 odds=191/191
2026-07-24 17:09:18,903 [INFO] predictor: CALIBRATION_MODE=on
2026-07-24 17:09:18,903 [INFO] predictor: combos: {'win': 6, '2t': 30, '3t': 120}
2026-07-24 17:09:18,906 [INFO] run_cycle: fetched 22/11 [scan]: 156 combos
2026-07-24 17:09:19,015 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 87
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 87
  }
]
```

## Phase別通知記録 (24h)
{'final': 34, 'result': 20, 'scan': 33}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 139
  FINAL_MISSING: 99
  CIRCUIT_BREAKER_TRIP: 38
  CIRCUIT_BREAKER_NO_ACTION: 34
  STRATEGY_CI_FAIL: 17
  ANOMALY_SCAN_FINAL_RATIO: 14
  LARGE_ODDS_DRIFT: 2
  ANOMALY_BET_VOLUME_SPIKE: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 51 | 12 | 15,300 | 11,130 | -4,170 | 0.727 |
| S01_NAKAANA1 | 40 | 8 | 8,000 | 5,760 | -2,240 | 0.72 |
| S02_TETSUBAN | 16 | 9 | 3,200 | 3,220 | +20 | 1.006 |

## 直近アラート (24h・新しい順)
```
[17:09:19] FINAL_MISSING: {"deadline": "2026-07-24T14:37:00+09:00", "kind": "FINAL_MISSING", "nid": "2026072406071437", "sid": "S00"}
[17:06:30] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[17:06:30] FINAL_MISSING: {"deadline": "2026-07-24T12:33:00+09:00", "kind": "FINAL_MISSING", "nid": "2026072406031233", "sid": "S00"}
[17:06:30] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S01_NAKAANA1"}
[17:06:30] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S00"}
[16:53:26] FINAL_MISSING: {"deadline": "2026-07-24T12:21:00+09:00", "kind": "FINAL_MISSING", "nid": "2026072413051221", "sid": "S00"}
[16:49:04] FINAL_MISSING: {"deadline": "2026-07-24T15:18:00+09:00", "kind": "FINAL_MISSING", "nid": "2026072412011518", "sid": "S00"}
[16:49:04] FINAL_MISSING: {"deadline": "2026-07-24T11:16:00+09:00", "kind": "FINAL_MISSING", "nid": "2026072402021116", "sid": "S00"}
[16:33:19] FINAL_MISSING: {"deadline": "2026-07-24T15:03:00+09:00", "kind": "FINAL_MISSING", "nid": "2026072417091503", "sid": "S00"}
[16:33:19] FINAL_MISSING: {"deadline": "2026-07-24T13:02:00+09:00", "kind": "FINAL_MISSING", "nid": "2026072403051302", "sid": "S00"}
```

## 本日残レース: 47件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 180件 登録 / 133件 締切済
- 通知発射: scan=29 nid / final=28 nid / result=15 nid
- predictions: 16 / うち結果DB記録済: 16
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 9件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S00 | 153R | win | 1 | 0.1957 | 14.2 | 2.78 | 300 | scan=- drift=- | 16:31:30 |
| S02_TETSUBAN | 1310R | win | 1 | 0.5039 | 2.6 | 1.31 | 200 | scan=- drift=- | 15:08:30 |
| S00 | 225R | win | 1 | 0.4111 | 4.5 | 1.85 | 300 | scan=- drift=- | 14:15:43 |
| S01_NAKAANA1 | 028R | win | 1 | 0.5891 | 3.8 | 2.24 | 200 | scan=4.0 drift=-5.0% | 14:13:18 |
| S00 | 026R | win | 1 | 0.5735 | 12.9 | 7.40 | 300 | scan=- drift=- | 13:11:54 |
| S01_NAKAANA1 | 1410R | win | 1 | 0.5123 | 3.4 | 1.74 | 200 | scan=- drift=- | 13:02:19 |
| S01_NAKAANA1 | 033R | win | 1 | 0.5124 | 4.8 | 2.46 | 200 | scan=- drift=- | 12:05:19 |
| S00 | 084R | win | 1 | 0.3177 | 20.0 | 6.35 | 300 | scan=6.7 drift=+198.5% | 12:02:19 |
| S00 | 023R | win | 1 | 0.4920 | 13.1 | 6.45 | 300 | scan=13.1 drift=+0.0% | 11:42:18 |
| S01_NAKAANA1 | 083R | win | 1 | 0.4111 | 4.5 | 1.85 | 200 | scan=4.1 drift=+9.8% | 11:33:44 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 53 | +26.7% | -83.7% | +628.9% | 19 | 9 | 40 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 459.8s |
| **Latency** (scan→final max) | 663.8s |
| **Traffic** (notifications 24h) | 87 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 2,700円 used |
| **Saturation** (S01_NAKAANA1) | 1,000円 used |
| **Saturation** (S02_TETSUBAN) | 400円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 422 | 0.4668 | 0.3199 | +0.1468 | 🟡+32% | 0.2354 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 181 | 0.4244 | 0.2818 | 0.2248 | 🔴-0.11 | 0.762 |
| S01_NAKAANA1 | win | 165 | 0.4789 | 0.2788 | 0.2389 | 🔴-0.19 | 0.772 |
| S02_TETSUBAN | win | 76 | 0.5413 | 0.5000 | 0.2530 | 🔴-0.01 | 0.984 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.10-0.15 | 6 | 0.1267 | 0.1667 | ✅-0.0400 |
| 0.15-0.20 | 8 | 0.1814 | 0.3750 | 🔴-0.1936 |
| 0.20-0.30 | 13 | 0.2273 | 0.3077 | 🔴-0.0804 |
| 0.30-0.50 | 168 | 0.4173 | 0.2798 | 🔴+0.1376 |
| 0.50+ | 224 | 0.5421 | 0.3571 | 🔴+0.1850 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 84 | 0.805 |
| win | <5.0 | ✅learned | 152 | 0.725 |
| win | <10.0 | ✅learned | 79 | 0.462 |
| win | <20.0 | ✅learned | 26 | 0.216 |
| win | <50.0 | ⚠️fallback | 6 | 0.1 |
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
_auto-generated by claude_snapshot.py at 2026-07-24T17:10:01.439576+09:00_